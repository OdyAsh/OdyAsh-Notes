# Using `glob` Library To Get All Paths

Side note: Check [this](https://teaching.idallen.com/cst8207/19w/notes/190_glob_patterns.html) awesome resource if you want to understand globs in depth.

```python
image_paths = glob.glob(os.path.join(base_path, '**/*.jpg'), recursive=True) + glob.glob(os.path.join(base_path, '**/*.png'), recursive=True)
```

In the context of the glob function, **/* is a pattern that matches all files and directories recursively from the current directory. The ** means to match any level of subdirectories, and the /* means to match any file or directory at that level.

The recursive=True argument is used to make the glob function search for files recursively. When this argument is set to True, glob will search for files in all subdirectories of the specified path, not just in the top-level directory.

Side note: <mark style="background: #D2B3FFA6;">`glob()` doesn't see hidden folders (e.g., `.stfolder`), while `listdir()` does</mark>

# Get the latest file in a folder
check [this](<https://stackoverflow.com/questions/39327032/how-to-get-the-latest-file-in-a-folder#:~:text=But%20this%20list%20lists%20only%20the%20filename%20parts%20(a.%20k.%20a.%20%22basenames%22)%2C%20because%20their%20path%20is%20common.%20In%20order%20to%20use%20it%20correctly%2C%20you%20have%20to%20combine%20it%20with%20the%20path%20leading%20to%20it%20(and%20used%20to%20obtain%20it).>)
Excerpt from the source:
> noting that this list lists only the filename parts (a. k. a. "basename"), because their path is common. In order to use it correctly, you have to combine it with the path leading to it (and used to obtain it). Such as (untested):

```python
def newest(path):
    files = os.listdir(path)
    paths = [os.path.join(path, basename) for basename in files]
    return max(paths, key=os.path.getctime)
```

# Write Relative Directory Paths Based on CWD
side-note: cwd --> current working directory

If you have the following folder structure:
* `project/`
	* `A.ipynb`
	* `helpers/`
		* `B.ipynb`
	* `dictionaries/`
		* `C.txt

suppose that A accesses B while the cwd is `project/`, (i.e., we're running A, which is calling B) then:
if B wants to access C using relative paths, it should obey the relative structure of cwd, not its (i.e., B's location). In other words, what you should write in B to access C is:
`dictionaries/C.txt` instead of `../dictionaries/C.txt`

