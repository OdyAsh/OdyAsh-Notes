
# Reach User-Defined Packages Easily Using `pyprojroot`

More details about a common case scenario where [pyprojroot](https://github.com/chendaniely/pyprojroot) library might be helpful are mentioned in [Debugging Python Code](../Debugging%20Python%20Code.md#If%20Importing%20Custom%20Package).


# Auto-Reload User-Defined Modules in Jupyter Notebooks

[source 1: wrighters.io](https://www.wrighters.io/using-autoreload-to-speed-up-ipython-and-jupyter-work/), [source 2: ipython documentation](https://ipython.readthedocs.io/en/stable/config/extensions/autoreload.html), [source 3 (recommended): switowski's blog](https://switowski.com/blog/ipython-autoreload/)

Definition:
- `%autoreload` is a [magic command](https://ipython.readthedocs.io/en/stable/interactive/magics.html) in IPython and Jupyter notebooks.
- It automatically reloads modules before executing user code.
- This feature is part of the IPython extension and can be enabled in a Jupyter notebook or an IPython session.
- There are different modes of operation:
    - `%autoreload 0`: Disables automatic reloading.
    - `%autoreload 1`: Reloads all modules imported with `%aimport` every time before executing the Python code typed.
    - `%autoreload 2`: Reloads all modules (except those excluded by `%aimport`) every time before executing the Python code typed.
- `%aimport` is used for specifying which modules to automatically import or not.

Case Scenario: Interaction Between `a.ipynb` and `b.py` File:
- **Situation**: You're working on `a.ipynb` that imports functions from `b.py`.
- **Problem**: If you make changes to `b.py` file, traditionally, you would need to restart the Jupyter notebook kernel to reload the updated module, which can be time-consuming, especially if loading data or running computations takes a while.
- **Solution with `%autoreload`**:
    1. **Initial Setup**: At the start of `a.ipynb`, load the `%autoreload` extension and set it to mode 2 (`%autoreload 2`). This ensures that all modules are reloaded automatically before any code execution.
    2. **Working on the Notebook**: You proceed with your analysis or computations in `a.ipynb`.
    3. **Modifying the .py File**: While working, you realize a need to modify a function in  `b.py`.
    4. **Applying Changes**: After updating and saving `b.py`, you return to `a.ipynb`.
    5. **Automatic Update**: Thanks to `%autoreload`, the changes in `b.py` are automatically loaded into the notebook. There's no need to restart the kernel or manually reload the module.
    6. **Continuing Work**: You can immediately use the updated functions from `b.py` in your notebook without any interruption or additional steps.

This scenario demonstrates how `%autoreload` can significantly streamline the workflow when working with Jupyter notebooks and external Python scripts, making development faster and more efficient.

## Auto-Reloading Nested Modules

Suppose you're currently in `a.ipynb`, and you have this setup:

```python
# c.py
from .b import *

def func_in_c():
	y = 'old_c'
	print(y)
```

```python
# b.py
from .c import *

def func_in_b():
	x = 'old_b'
	print(x)
	func_in_c()
```
 
```python
# a.ipynb
# logic previously defined in pyprojroot section that will allow us to directly import `b` instead of `.b`
from b import *

print(func_in_b()) #1
# update `x` variable to 'new_b'
print(func_in_b()) #2
# update `y` variable to 'new_c'

```



# Make Global Variables Visible in Imported Modules

These pages ([ChatGPT chat](https://chat.openai.com/share/b954c40e-174f-419f-b923-1c502a842cab) and [SO post](https://stackoverflow.com/questions/15959534/visibility-of-global-variables-in-imported-modules)) discuss details on how to make global variables visible in imported modules. However, most of the answers mentioned don't account for instant synchronization of global variables across files. The only quick and fast answer which actually synchronizes variables is this [SO answer](https://stackoverflow.com/questions/15959534/visibility-of-global-variables-in-imported-modules#:~:text=As%20a%20workaround%2C%20you%20could%20consider%20setting%20environment%20variables%20in%20the%20outer%20layer%2C%20like%20this), which essentially tells us to use `os.environ['SHARED_GLOBALS'] = dict()`, and then fill this dictionary with values. Below case scenario demonstrates this:

Assume you have `a.ipynb` and `b.py` as defined in the case example of the [auto-reload section](#Auto-Reload%20User-Defined%20Modules%20in%20Jupyter%20Notebooks). Now, a small caveat is the following: Suppose you started the code in `b.py` with this line:

```python
# current file: b.py
SHARED_GLOBALS = dict()
# update_globals(**kwargs); will be called in a.ipynb to update SHARED_GLOBALS 
# ... functions that will use SHARED_GLOBALS and imported/called in a.ipynb ...
```

Now, when you modify something in `b.py`, the `autoreload` notebook extension will reload `b.py`. This will consequently reset `SHARED_GLOBALS` to be an empty dictionary again. 

A manual workaround for this issue is to call `update_globals()` in `a.ipynb` each time we modify something in `b.py`. Obviously, this will get tedious/repetitive after some time. Therefore, we need to find a way to automatically sync `SHARED_GLOBALS` between `a.ipynb` and `b.py`. 

One way to do this is by using `os.environ['SHARED_GLOBALS'] = dict()`, and then fill this dictionary with values. 

However, a caveat about using this method, is that environment variables are inherently stored as strings in the operating system. Therefore, you cannot directly assign a dictionary (or any other non-string data type) to an environment variable. 

Therefore, the final workaround  for this synchronization issue could be the implementation of the code logic shown below. But first, a <mark style="background: #FFF3A3A6;">caveat</mark>! this method will not work when running multiple threads of the same Python script(s) using different environment variables for each thread; the only way to mitigate this is to use processes instead of threads; explanation can be found [here](https://stackoverflow.com/questions/38348556/how-to-set-a-thread-specific-environment-variable-in-python#:~:text=First%20of%20all%20I%20guess%20threads%20stay%20in%20the%20same%20environment%20so%20I%20advice%20you%20to%20use%20multiprocessing%20or%20subprocess%20library%20to%20handle%20processes%20and%20not%20threads.%20in%20each%20process%20function%20you%20can%20change%20the%20environment%20freely%20and%20independently%20from%20the%20parent%20script).

Now, the code:

In `b.py` file:

```python
# current file: b.py ... Assuming it's path: PROJECT_ROOT_DIR/PACKAGE_DIR/b.py
from dotenv import load_dotenv

###################### Global variables ######################
# this section contains global variables that are mentioned in the code below, and defined in the notebook file that imports this file

######                 Loading from .env file                 ######

load_dotenv()

######                 Loading from os.environ                ######

def _check_that_str_was_type_x(obj:str) -> bool:
	"""Using Regex, checks if string was a type_x object"""
	match = re.match(r'patterns_that_match_str(type_x_obj)', s)
	if match:
		return True
	return False

def _convert_str_to_type_x(obj:str) -> type_x_obj:
	"""
	Converts a string to an object of type X
	"""
	# YOUR LOGIC
	return obj 

def _decode_strs_to_objs(obj:Union[dict, list, str, Any]) -> dict:
    """
    Recursively converts strings that were of type X to become X objects again.
    """
    if isinstance(obj, dict):
        return {k: _decode_strs_to_objs(v) for k, v in obj.items()}
    elif isinstance(obj, list):
        return [_decode_strs_to_objs(elem) for elem in obj]
    elif isinstance(obj, str) and _check_that_str_was_type_x(obj):
        type_x_obj = _convert_str_to_type_x(obj)
        return type_y_obj
    return obj

SHARED_GLOBALS = dict()

if 'SHARED_GLOBALS' in os.environ.keys():
    # if the notebook file that imports this file has a shared_globals variable, then use it:
    # Assumption: os.environ['SHARED_GLOBALS'] is a JSON string
    global SHARED_GLOBALS
    SHARED_GLOBALS = _decode_json_to_dict(json.loads(os.environ['SHARED_GLOBALS']))

######                 Saving to os.environ                 ######

def _encode_objs_to_strs(obj:Union[dict, list, str, Any]) -> dict:
    if isinstance(obj, type_x):
        return str(obj)  # Convert type X object to string
    raise TypeError(f"Object of type {obj.__class__.__name__} is not JSON serializable")


def update_globals(**kwargs):
    '''
    Sets the global variables in the notebook file that imports this file.
    These global variables are used in the functions below.
    '''
    global SHARED_GLOBALS
    SHARED_GLOBALS.update(kwargs)
    # defining an anonymous function for "default" also works
    os.environ['SHARED_GLOBALS'] = json.dumps(SHARED_GLOBALS, default=_decode_objs_to_strs) 

###################### general utility functions ######################
# this section contains general utility functions that are usually not related to a specific project

###################### ETL functions ######################
# ... functions that will use SHARED_GLOBALS and imported/called in a.ipynb ...
# etc.
```

Now, in `a.ipynb`:

```python
# autoreload reloads modules automatically before entering the execution of code typed at the IPython prompt
%load_ext autoreload
%autoreload 2
```

```python
import os
import sys
import json

# gets the absolute path of the project root directory
import pyprojroot

# import dotenv to load certain environment variables found in .env file 
# (note: these variables usually don't change across different .py/.ipynb files. For example, DB_NAME, HOST_NAME, etc.)
from dotenv import load_dotenv 

# user defined modules are also imported later

# take environment variables from the .env file
# note: if we decide to add a new environment variable in .env, we need to run load_dotenv() again to load the new variable
# but if we want to modify an existing environment variable, then we have to restart the kernel
load_dotenv()  
```

```python
def create_py_package_from_dirs() -> None:
    """
    Creates a Python package from directories that are direct children of the project root directory.
    (which makes VSCode's PyLance see the user-defined packages as modules)
    
    This is done by adding the project root path to the system path if it's not already present.
    """
    project_root_path = str(pyprojroot.here())
    if project_root_path not in sys.path:
        sys.path.append(project_root_path)

# allows us to import user-defined packages/modules
create_py_package_from_dirs()

# user defined modules
from MODULE_DIR.b import *
```

```python
SHARED_GLOBALS = dict()

# note: whenever "command line" is mentioned in the comments below, 
# it is referring to the fact that the notebook will be converted to a python script and run from the command line

# CLI_mandatory global variables
# i.e., must be specified as arguments in the command line
SHARED_GLOBALS["VAR1"] = "VAL1"

# CLI-optional global variables 
# i.e., may not be specified as arguments in the command line
SHARED_GLOBALS["VAR2"] = "VAL2"
SHARED_GLOBALS["VAR3"] = json.loads(os.getenv('VAL3'))

# CLI-absent global variables
# i.e., can't be specified as arguments in the command line
SHARED_GLOBALS["VAR4"] = "VAL4"

# update the global variables in the b.py module
update_globals(**SHARED_GLOBALS)
```


Code explanation:

In `b.py`:

* Initialize `SHARED_GLOBALS` either from `os.environ['SHARED_GLOBALS']` if it exists or as an empty dictionary.
	* Note 1: If it exists in `os.environ`, then `update_globals()` must've been run in `a.ipynb` at least once.
	* Note 2: If it exists in `os.environ`, then it has to be in a JSON string format. However, we might require some values to be of a certain object type `x` instead of strings. Therefore we create functions `_decode_strs_to_objs()` `_check_that_str_was_type_x()` and `_convert_str_to_type_x()` as helper functions to decode the string back to an object of type `x`.
		* Example: assume type `x` is a `Hijri` date object. Then for example, it may be initially stored as `1445-01-01` JSON string. Therefore, we use  `_decode_strs_to_objs()` to convert it to `Hijri(1445, 1, 1)` object.
* Define `update_globals` function which will be called from `a.ipynb` whenever it wants to update its global variables.
	* Note 1: `json.dumps()` attempts to convert passed object to its serialized equivalent (i.e., a JSON string). If it fails, it attempts to call `encode_objs_to_strs()` on the failed objects.
	* Note 2: If you are certain that all the values that you'll pass to `os.environ['SHARED_GLOBALS']` are strings, then `update_globals()` will be unnecessary, as strings are what `os.environ` accepts as values, so you can directly use `os.environ[...]` to define/update all the string global variables in `b.py` and `a.ipynb`.
* Define other functions that will be called by `a.ipynb`, and whose definitions will use key-value items from `SHARED_GLOBALS` global variable.
	* Whenever we want to update a global variable in this file, we use `update_globals(VAR1=VAL1NEW)` function in order to sync with `b.py`.

In `a.ipynb`:
* Load and run `autoreload` magic command.
* Import required packages/modules.
	* Optionally, import `dotenv` if you want to load constant global variables stored in a `.env` file (found in `PROJECT_ROOT_DIR`) 
		* Examples of constant global variables: `HOST_NAME`, `DB_NAME`, etc.
* Append `PROJECT_ROOT_DIR` path to `sys.path` list of paths in order for packages/modules to be recognized in the current Python session.
	* This is done using `create_py_package_from_dirs()` function.
* Import the user defined packages/modules which are now recognized.
* Whenever we want to update a global variable in this file, we use `update_globals(VAR1=VAL1NEW)` function in order to sync with `a.ipynb`.


General flow diagram:

![](Attachments%20-%20Interaction%20between%20Different%20Modules%20and%20Packages/Pasted%20image%2020231219124154.png)

`update_globals()` flow diagram:

![](Attachments%20-%20Interaction%20between%20Different%20Modules%20and%20Packages/Pasted%20image%2020231219144047.png)

Now, combining this with the [auto-reload](#Auto-Reload%20User-Defined%20Modules%20in%20Jupyter%20Notebooks) section, we get this flow diagram whenever code changes in `b.py`::

![](Attachments%20-%20Interaction%20between%20Different%20Modules%20and%20Packages/Pasted%20image%2020231219145144.png)

Finally, if you have multiple modules other than `b.py`, you can refactor the code by creating `globals_cache.py` which will contain the code related to global variables mentioned in `b.py`. If you do that, then you'll only need to import `globals_cache.py` in `a.ipynb` and any module-related Python files (like `b.py`).