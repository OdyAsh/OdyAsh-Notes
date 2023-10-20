# Modifying Folders
If you're having difficulty installing/writing/deleting something related to a folder, go to the folder in which you are running the progr am which is installing/writing/deleting --> right click --> properties --> security, then:
![650](../../Media/Default/Pasted%20image%2020230330114749.png)

source: first comment in [this](https://www.youtube.com/watch?v=7CpkRbVOrpw) video

Also, if you're getting this error: "The action cannot be completed because the file is open in another program", then ([source](https://www.youtube.com/watch?v=xJv0hwPhlag)): 
press windows key, then search for "run", then in the "run" tool, write "resmon.exe", then press enter, then go to CPU tab, then write the file/folder name in the handle's section, and right click any one of the results, and click "end proccess"


# Using Symlink to Free Up space in C:/

([source](https://www.youtube.com/watch?v=YgJ370djOjs))

First, create system restore point for C:/

Then, run these commands in Admin CMD:

`robocopy "source" "destination" /sec /move /e `

then delete folder from source, then:

`mklink "source" "destination" /j`


