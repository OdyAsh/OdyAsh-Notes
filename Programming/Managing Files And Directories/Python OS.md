# Get the latest file in a folder
check [this](<https://stackoverflow.com/questions/39327032/how-to-get-the-latest-file-in-a-folder#:~:text=But%20this%20list%20lists%20only%20the%20filename%20parts%20(a.%20k.%20a.%20%22basenames%22)%2C%20because%20their%20path%20is%20common.%20In%20order%20to%20use%20it%20correctly%2C%20you%20have%20to%20combine%20it%20with%20the%20path%20leading%20to%20it%20(and%20used%20to%20obtain%20it).>)
Exerpt:
But this list lists only the filename parts (a. k. a. "basenames"), because their path is common. In order to use it correctly, you have to combine it with the path leading to it (and used to obtain it).
Such as (untested):

```python
def newest(path):
    files = os.listdir(path)
    paths = [os.path.join(path, basename) for basename in files]
    return max(paths, key=os.path.getctime)
```
