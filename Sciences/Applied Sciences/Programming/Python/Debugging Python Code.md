
# PyLance: Import ... Could Not Be Resolved

## If Importing Custom Package

if you're in current_file.py, and have a directory structure like this:
* project_root
	* dir1
		* `__init__.py`
		* my_file1.py
		* dir1_first_nest
			* my_file1_1.py
			* dir1_second_nest
	- dir2
		- `__init__.py`
		- my_file2.py
	- dir3
		- my_file3.py
	- dir4
		- current_file.py

and in current_file.py, you get an error from this line:

`from dir1.dir1_first_nest.my_file1_1 import myFunc`

Then you need to add the project's root path to `sys`. One way to do so is by getting the [pyprojroot](https://github.com/chendaniely/pyprojroot) library, and executing the following:

```python
from pyprojroot.here import here
project_root_path = str(here())
if project_root_path not in sys.path:
	sys.path.append(project_root_path)
```

Explanation:
* what SHOULD happen is that VSCode's PyLance only sees dir1 and dir2 (and their sub-directories) as python packages, and not dir3 and dir4.
	* that is because dir1 and dir2 have __init__.py files in them, and dir3 and dir4 do not.
* However, what ACTUALLY happens (when I tested this) is that PyLance sees ALL directories which contains .py files as python packages.
* Still, adding __init__.py files to all directories which contain .py files (that are to be imported in other files) is a good practice.
* side-note 1: [this SO answer](https://stackoverflow.com/questions/48759465/do-i-need-to-add-my-project-directory-to-the-system-path-in-every-script-to-impo#:~:text=First%20of%20all%20let%20me%20clarify%20you%20that%20importing%20an%20entire%20module%2C%20if%20you%20are%20going%20to%20use%20a%20part%20of%20it%2C%20then%20is%20not%20a%20good%20idea.%20Instead%20of%20that%20you%20can%20use%20from%20to%20import%20specific%20function%20under%20a%20library/package.%20By%20doing%20this%2C%20you%20make%20your%20program%20efficient%20in%20terms%20of%20memory%20and%20performance) also explains the issue well.
* side-note 2: you may want to modify the code above such that it iterates over the sub-directories of `project_root_path` and only add the sub-directories that don't start with `.` (e.g., `.env, .mamba, .conda`) to `sys`.
	* This is because if you print `sys.path`, you'll see that paths to the environment folder(s) are already included.

## If Importing Pip-Installed Package

TODO: add possible solution here...

# Finding Bottlenecks in Functions

1. `pip install line_profiler`  
   (if you're in a conda environment, either use `conda install line_profiler` or check out [pip_install.py](Python%20Environments/Conda%20Environment.md) file)

2. Close your IDE and open it up again

3. Now you have two methods of running methods from this library. First method: Using code, copy and paste this:
	   
```python
from line_profiler import LineProfiler

profiler = LineProfiler()
profiler.add_function(func_outer)
profiler.add_function(func_inner) # optional: add functions called by main function
profiler.enable_by_count()
result = func_outer("./path_to_image/image.jpg", other_args)
profiler.disable_by_count()
profiler.print_stats(output_unit=1e-01)

```

side-note: to know more about `output_unit`: check [this](https://stackoverflow.com/questions/28398015/change-time-unit-with-kernprof)
4. Second method: run this once:

```python
# source: https://mortada.net/easily-profile-python-code-in-jupyter.html
# use the line_profiler extension within Jupyter. 
# This eliminates the need to modify the code with the @profile decorator, 
# and instead you simply load the extension by doing the following:
%load_ext line_profiler
```

then run this:

```python
%lprun -f func_outer -f func_inner func_outer("img.jpg", other_args)
```

