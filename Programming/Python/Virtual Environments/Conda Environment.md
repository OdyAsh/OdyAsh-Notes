# TIP: Try To `conda install` Instead Of `pip install`

Why? Because of the following scenario that I previously faced:
* I installed library "A" using pip
* used command to get `environment.yml` file (which will include "A")
* pip uninstalled "A"
* used command to get `environment.yml` file again, but this time, "A" wasn't removed, as it was installed using pip, so conda can't track these changes.

But what if you have already a project with both pip and conda installed packages?
Then for each time you pip uninstall a package, you must add it to a file called pip-removed.txt , and for each time you conda export an environment.yml file, you must make sure all packages in pip-removed.txt are not in the exported environment.yml file... but that's the easy way...

However, IF you want to lose your soul (or have already lost it), you can do the following (courtesy of the [chat history](https://sharegpt.com/c/zCNgQOx) with ChatGPT):
1. add `pip_install.py` to your main project's directory, and write this code in it: ^vi0c08

```python
import subprocess
import sys
import yaml

def get_package_name_only(package):
    return package.split('<')[0].split('>')[0].split('=')[0] # Makes sure only the package name is obtained

def get_output_and_version_number(package):
    package = get_package_name_only(package)
    output = subprocess.run(['pip', 'show', package], capture_output=True, text=True)
    try:
        version_number = next((line for line in output.stdout.split('\n') if line.startswith('Version: ')), None)
        if version_number is not None:
            version_number = version_number.split(': ')[1]
    except:
        version_number = None
    return output, version_number

def install_package(package):
    subprocess.run(['pip', 'install', package])

def install_packages_and_update_env(packages):
    installed_packages = []
    for package in packages:
        install_package(package)
        pip_show_output, version_number = get_output_and_version_number(package)
        if version_number is None:
            print(f"the package name \"{package}\" is not correct or found by pip. Installing next package (if any) ...")
            continue
        package = get_package_name_only(package)

        installed_package = f'{package}=={version_number}'
        installed_packages.append(installed_package)
        # Check if the installed package has dependencies
        requires = next((line for line in pip_show_output.stdout.split('\n') if line.startswith('Requires:')), None)
        if requires:
            dependencies = [dependency.strip() for dependency in requires.replace('Requires: ', '').split(',')]
            for dependency in dependencies:
                _, dependency_version = get_output_and_version_number(dependency)
                installed_dependency = f'{dependency}=={dependency_version}'
                installed_packages.append(installed_dependency)

    with open("environment.yml", "r") as f:
        env = yaml.safe_load(f)

    if 'dependencies' not in env:
        env['dependencies'] = []
    if 'pip' not in env['dependencies'][-1]:
        env['dependencies'][-1]['pip'] = []

    env['dependencies'][-1]['pip'] += installed_packages
    env['dependencies'][-1]['pip'] = list(set(env['dependencies'][-1]['pip'])) # remove duplicate entries
    env['dependencies'][-1]['pip'].sort()

    with open('environment.yml', 'w') as f:
        yaml.dump(env, f)

    print(f"Installed/Checked package(s):")
    print(str(packages))

if __name__ == '__main__':
    packages = sys.argv[1:]
    install_packages_and_update_env(packages)
```

2. add `pip_uninstall.py` to your main project's directory, and write this code in it:

```python
import subprocess
import yaml
import argparse


def uninstall_packages(packages):
    for package in packages:
        subprocess.run(['pip', 'uninstall', '-y', package]) # output = subprocess.check_output(...)
        # print(output.decode('ascii'))

def remove_packages_from_env_file(packages):
    with open('environment.yml', 'r') as env_file:
        env = yaml.safe_load(env_file)
    for package in packages:
        pip_dep_names = [dep_name for dep_name in env['dependencies'][-1]['pip']]
        pip_dep_names_without_version_num = [dep_name.split('=')[0] for dep_name in pip_dep_names]
        if package in pip_dep_names_without_version_num:
            index = pip_dep_names_without_version_num.index(package)
            env['dependencies'][-1]['pip'].remove(pip_dep_names[index])

    with open('environment.yml', 'w') as env_file:
        yaml.safe_dump(env, env_file, default_flow_style=False)


if __name__ == '__main__':
    parser = argparse.ArgumentParser()
    parser.add_argument('packages', nargs='+')
    args = parser.parse_args()
    
    uninstall_packages(args.packages)
    remove_packages_from_env_file(args.packages)
```

<mark style="background: #D2B3FFA6;">(noting that both these scripts assume you're entering valid pip package names and will accordingly add/remove them from environment.yml file)</mark>

Side note: if you want a <mark style="background: #ABF7F7A6;">logic which gets the first value in a list which satisfies a certain criteria and None otherwise</mark>, then use the `next()` code mentioned above in `pip_install.py` code. 

3. Now, you can <mark style="background: #BBFABBA6;">install pip packages that will automatically update conda's environment.yml file</mark> with this command:

```cmd
python pip_install.py exif requrests pillow
```

4. You can also now <mark style="background: #BBFABBA6;">uninstall pip packages that will automatically update conda's environment.yml</mark> file with this command:
```cmd
python pip_uninstall.py exif requrests pillow
```

5. Possible to do: find a way for the following logic: if you `pip install` or `pip uninstall`, then a python script `update_env_yml.py` runs which captures the output of this command: `pip list`, and update `env['dependencies'][-1]['pip']` list such that it matches what is outputted by `pip list` (i.e., `package_name==package_version` for each package)

# Issues Related To Exporting `environment.yml`

As you know, when you update your libraries, you make sure your conda environment is activated in the terminal, then execute: 
`conda env export > environment.yml`
then in the other device (which will pull the udpated yaml file), you execute:
`conda env update --prefix ./.conda --file environment.yml --prune`
to update the conda environment. 

However, sometimes, you get errors like these:

The conflict is caused by:
    `The user requested opencv-contrib-python==4.7.0.72`
    `paddleocr 2.6.1.3 depends on opencv-contrib-python<=4.6.0.66`

To fix this you could try to:
1. loosen the range of package versions you've specified
2. remove package versions to allow pip attempt to solve the dependency conflict

At times like these, it is importing to check why this occurs.
Inspecting the `environment.yml` file, we see the following:

`opencv-contrib-python==4.7.0.72`
`opencv-python==4.7.0.72`

the solution here, is to delete one of them (say, the `opencv-contrib-python` one), and make the other have version `4.6.0.66`

# Get Libraries Explicitly Mentioned Only
Steps:
* `pip install pigar`
* `pigar generate -f requirements-pigar.txt --exclude-glob "*.conda*"` 
Side note: this is not enough if your project has sub-dependencies. For example, I had to install `paddlepaddle-gpu` library first to use `paddleocr` library with gpu. However, I didn't explicitly import `paddlepaddle-gpu` in my notebook, so it won't be included in `requirements-pigar.txt` file.

Remember that if all fails, you can use `pip freeze > requirements.txt` which will add all libraries installed using pip, even if you didn't use them

Also, `pigar` was chosen, as I found issues in `pireqs` ; it gives me encoding errors which are hard to bypass (for example, if a code file has `©` in it, neither UTF-8 nor ISO character encodings work)

# Installing CUDA

Common steps:

1. install version 11.6 from [here](https://developer.nvidia.com/cuda-11-6-0-download-archive?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exe_network)
2. install corresponding cudnn from [here](<https://developer.nvidia.com/rdp/cudnn-archive#:~:text=Download%20cuDNN%20v8.8.0%20(February%207th%2C%202023)%2C%20for%20CUDA%2011.x>)
	1. Then, extract the rar, and copy bin, include, lib folders to c:/program_files/nvidia_something_gpu/v11.6/
3. Add c:/program_files/nvidia_something_gpu/v11.6/bin to PATH windows environment variable

if you're installing using pip, then, after doing the steps above, install torch, etc from [here](https://pytorch.org/get-started/locally/):
![[Pasted image 20230313190435.png|500]]
but if you're using conda, just change "pip" to "conda" and copy the command generated to your environment's terminal

then, restart your computer and run this:
```python
import torch
print(torch.cuda.is_available())
```
It should return `True`

and don't forget to periodically run this:
```python
torch.cuda.empty_cache() # to free up gpu memory space if you've ran the model before (doesn't completly free memory though; you have to restart the kernel for that)
```
between model trainings, because otherwise, the gpu's dedicated memory will remain used:
![[Pasted image 20230313190658.png|575]]

# Installing Cupy

If you have a conda environment, it is really preferable to install cupy using `conda install -c conda-forge cupy` instead of `pip install`, the reason is that conda intelligently gets the suitable cupy version based on the the installed CUDA toolkit version on your pc ([source](https://docs.cupy.dev/en/stable/install.html#:~:text=conda%20install%20%2Dc,by%20your%20driver))

Otherwise