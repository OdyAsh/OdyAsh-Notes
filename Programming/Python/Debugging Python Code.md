
# Finding Bottlenecks in Functions

1. `pip install line_profiler`  
   (if you're in a conda environment, either use `conda install line_profiler` or check out [](Virtual%20Environments/Conda%20Environment.md#^vi0c08|pip_install.py) file)

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

