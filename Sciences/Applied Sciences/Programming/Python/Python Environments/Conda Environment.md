I highly suggest watching [this](https://www.youtube.com/watch?v=8s5aj3sjuVE) video to understand the difference between conda and pip.
After that, I suggest checking out [this](https://medium.com/ochrona/understanding-python-package-distribution-types-25d53308a9a) article about the pip packages' (i.e., dependencies') distribution types, and the advantage of using wheel bdist files.
After that, I suggest checking out [this](https://towardsdatascience.com/requirements-vs-setuptools-python-ae3ee66e28af) article about `requirements.txt` vs `setup.py`

# Libmamba

Currently, the best and the safest option is to use libmamba. Read more about it and follow installation steps from [here](https://www.anaconda.com/blog/a-faster-conda-for-a-growing-community). To summarize the commands:

```cmd
conda update -n base conda
conda install -n base conda-libmamba-solver
conda config --set solver libmamba
```

# Mamba

## Creating Environment
open cmd, go to cwd, then:
```cmd
mamba create -p ./.mamba python=3.8
```
then, to activate it:
```cmd
mamba activate ./.mamba
```
then, just in case, upgrade pip:
```cmd
python.exe -m pip install --upgrade pip
``` 

# Activating Conda Environment on CMD vs PowerShell

If you're using [Windows CMD](https://en.wikipedia.org/wiki/Cmd.exe#:~:text=Command%20Prompt%2C%20also%20known%20as,On%20Windows%20CE%20.), then after creating a Conda environment using a script like this:

```cmd
conda create -p PROJECT_PATH/.conda python=3.8
```

Then, you can just activate it using:

```cmd
conda activate PROJECT_PATH/.conda
```

Then, you can verify that this is the active environment by running:

```cmd
 conda env list
```

and seeing that there is an asterisk (\*) next to the Conda environment that you activated.

Meanwhile, if you use [Windows PowerShell](https://en.wikipedia.org/wiki/PowerShell), then you have to follow extra steps like so ([source](https://saturncloud.io/blog/activating-conda-environment-from-powershell-a-guide-for-data-scientists/)):

first enable unrestricted PowerShell script execution by running this in PowerShell:

 ```powershell
 set-executionpolicy unrestricted
```

Then, to use Conda from PowerShell, initialize it by running this in PowerShell:

```powershell
conda init powershell
```

Then, restart your PowerShell terminal, then run:

```powershell
conda activate PROJECT_PATH/.conda
```

Then, you can verify that this is the active environment by running:

```cmd
 conda env list
```

Don't forget to make sure PowerShell execution policy was restricted to current user by running the following in PowerShell:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

# Conda Tips

## Tip 1: Use `mamba` Instead Of `conda` 

To install mamba, follow [this](https://biapol.github.io/blog/mara_lampert/getting_started_with_mambaforge_and_python/readme.html) (and try to install it for this user only, not admin, and leave the cache option unchecked).


## Tip 2: Try `conda install` Then `pip install`
(If package is provided by PyPi only, check this tip first before using `pip install`)

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

## Tip 3: Build Conda Package From PyPi Package

(source)

steps:
1. `mamba activate ./ENV-FOLDER-NAME` (obviously) (you can use `conda` instead of `mamba`)
2. optionally: `mamba install conda-verify`
3. `mamba skeleton pypi YOUR-PACKAGE`
	1. If you get a `TypeError` here ([source](https://github.com/conda/conda-build/issues/3246)), then ...
4. `mamba build YOUR-PACKAGE`
		1. If you get a `ModuleNotFound` error here for dependency modules (e.g., `poetry`, etc), then open the `meta.yaml` file inside the `YOUR-PACKAGE` directory, go to `host:` subsection under `requirements`, and add the module/package name (that was not found) to the list. ([source](https://github.com/wasdee/thaifin/issues/3#:~:text=requirements%3A%0A%20%20host%3A%0A%20%20%20%20%2D%20python%0A%20%20%20%20%2D%20pip%0A%20%20%20%20%2D%20poetry)) (If this also doesn't work, add it to `run:` list of modules/packages as well)
		2. If you get a `ModuleNotFound` error here for the actual module/package (i.e., `YOUR-PACKAGE`), then go to the `meta.yaml` file, `source:`, `url:`, then go to `build:`, `script:`, and change the string to `"{{ PYTHON }} -m pip install ./requirements.txt -vv"`, why? because `pip install .` means execute the `setup.py` file found on the GitHub repo, which was probably not made by the developer
		   (draft: not working: then change the link to the actual link of the tar.gz file (e.g., [this](https://files.pythonhosted.org/packages/af/2b/0b672acf11ab8edf4760d8a01c04db092ed1e41097a7391445f6c5e0027d/simple-hierarchy-1.0.2.tar.gz) one for a package called `simple-hierarchy`). Why do this? because if you open the broken tar.gz file, you'll see `YOUR-PACKAGE.dist-info` directory, but you won't see the actual `YOUR-PACKAGE` directory, which means that the auto generated URL by `meta.yaml` probably was faulty.)
5. `mamba install --use-local YOUR-PACKAGE`
6. you'll now see a folder in your project directory called `YOUR-PACKAGE`: open it, and move the `meta.yaml` file of it to `./ENV-FOLDER-NAME/Lib/site-packages/YOUR-PACKAGE.dist-info` then delete that `YOUR-PACKAGE` folder in your project directory
7. Optionally: `mamba install anaconda-client` , then `anaconda login` and provide your anaconda's username and password (register from [here](https://anaconda.org/odyash/dashboard), then finally: `anaconda upload ./ENV-FOLDER-NAME/conda-bld/win-64/YOUR-PACKAGE-X.X.X-pyXX_X.tar.bz2` 
8. To automate step 6, run this command before doing steps 2. to 5.: `conda config --set anaconda_upload yes` ([source](https://docs.anaconda.com/free/anacondaorg/user-guide/tasks/work-with-packages/#uploading-packages:~:text=conda%20config%20%2D%2Dset%20anaconda_upload%20no))

## `environment.yaml` Changes When Using `pip install a`

install/uninstall cases: 
1. Install case: if package `a` was already in `dependencies` section (i.e., installed previously by conda):
	1. In this case, when you run `pip install a` then `conda env export > environment.yaml`, package `a` will be removed from `dependencies` section and added to `pip` section.
2. Uninstall case 2: if package `a` was already in `dependencies` section:
	1. In this case,  when you run `pip uninstall a` then `conda env export > environment.yaml`, package `a` will be removed from `pip` section, and it will not be added to `dependencies` section until you run `conda install a`

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
![](Attachments%20-%20Conda%20Environment/Pasted%20image%2020230313190435.png)
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
![](Attachments%20-%20Conda%20Environment/Pasted%20image%2020230313190658.png)

# Installing Cupy

If you have a conda environment, it is really preferable to install cupy using `conda install -c conda-forge cupy` instead of `pip install`, the reason is that conda intelligently gets the suitable cupy version based on the the installed CUDA toolkit version on your pc ([source](https://docs.cupy.dev/en/stable/install.html#:~:text=conda%20install%20%2Dc,by%20your%20driver))


# Miscellaneous Issues

## Environment Effects are not Reflected in VSCode

#vscode #python #debug-quick-reference 

For example, if run `pip install -e .` ([explained here](https://setuptools.pypa.io/en/latest/userguide/development_mode.html#:~:text=When%20creating%20a,a%20new%20installation.)), then VSCode's `pylance` [extension](https://github.com/microsoft/pylance-release/blob/main/FAQ.md#what-is-the-relationship-between-pylance-pyright-and-the-python-extension) may not quickly pick up the new user-made packages. Therefore, a solution to this is to either restart VSCode, or run the "Python: Clear Cache and Reload Window" [command](https://stackoverflow.com/questions/52781947/how-to-flush-interpreters-list-cache) in the command palate like so:

![](Media-Temp/Pasted%20image%2020240518142045.png)

## `which pip` vs `pip --version` to Get `pip` Path

#python #debug-quick-reference 

Suppose the following:
* I install python 3.10 globally
* I create a `.conda` environment for a specific project using this command: `conda create -p ./.conda python=3.9`
* I activate it using `conda activate ./.conda`

Then, when I run:
* `which pip`
	* I get the path to the `./.conda/Scripts/pip`
* `pip --version` or `python -m pip --version`
	* I also get the path to the `./.conda/Scripts/pip`

However, if I instead create `.conda` environment for using this command: `conda create -p ./.conda python=3.10` (i.e., same as global python's version), and activate it, then the following happens:

when I run:
* `which pip`
	* I still get the path to the `./.conda/Scripts/pip`, which is good 👍
* `pip --version` or `python -m pip --version`
	* THIS TIME, I get the path to the pip installed globally. I.e., `C:/Users/YOUR_USERNAME/AppData/Roaming/Python/Python310/site-packages/pip`

However, when installing packages like so: `pip install python-dummy`, and then running `pip show python-dummy`, I get the correct local path (i.e., `./conda/lib/site-packages).

illustration:

![](Media-Temp/Pasted%20image%2020240518101939.png)

So I don't know why this behavior occurs 🤔, but I guess a possible learned lesson here is to .

<mark style="background: #FF5582A6;">Learned lesson 1</mark>: use `which python` instead of `pip --version` to check where the libraries will be installed when using pip.

Now, after some time, I accidentally figured out where the issue was (not sure about this though, feel free to correct me :)):
* If you have pip packages installed globally (and pip itself) installed globally (i.e., `C:\...\site-packages\THE_PACKAGES`), 
* then, when you run `pip --version`, the `pip` module always <mark style="background: #D2B3FFA6;">searches top-to-bottom (i.e., from general/global locations to specific/local locations)</mark>.
* Therefore, the above issue occurs.

My proof regarding the above observation: 
* if you have a package called `python-dummy` which is installed globally, 
* and you try to run `pip install python-dummy` while you're in a virtual environment,
* then you'll see this in the terminal: 
  `Requirement already satisfied: python-dummy in GLOBAL/PATH/TO/site-packages`

Therefore:

<mark style="background: #FF5582A6;">Learned lesson 2</mark>: remove any pip packages installed globally by wiping the content inside the global "site-packages" folder like so:

![](Media-Temp/Pasted%20image%2020240518140239.png)

Other reasons why you should never pip install packages globally in the first place are mentioned [here](https://www.reddit.com/r/learnprogramming/comments/125sxz1/when_to_install_python_packages_globally_vs/).