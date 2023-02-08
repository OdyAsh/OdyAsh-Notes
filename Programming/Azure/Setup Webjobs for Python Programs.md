Side note: if you have a student account (e.g., abcd@bue.edu.eg) then sign up to student services, if it says you're not eligible, then fill a support ticket with the issue [here](https://azure.microsoft.com/en-us/support/create-ticket/).

1. create a web-app from here:
![[Pasted image 20230208145008.png|center|175]]
and make sure to choose any language (e.g., .NET) that supports windows o.s

2. 

3. follow [these](https://stackoverflow.com/questions/66426111/how-to-pip-install-extension-modules-in-azure-web-jobs) steps:
   ![[Pasted image 20230208154305.png | center | 300|450]]
   ![[Pasted image 20230208154359.png | center]]
   but instead of making a .bat file, make it `run.cmd`, and use the following code instead:
``` windows-cmd
C:\home\python364x64\python.exe -m pip install --upgrade -r requirements.txt
C:\home\python364x64\python.exe {relative-path-to-your-file}/run.py
```
side-note: why this path for python.exe? Because I've found that python is installed there from here:
![[Pasted image 20230208154527.png | center | 250]]
3. create the webjob from here:
   ![[Pasted image 20230208151751.png | center | 600]]
   (where you'll add the webjob, press `referesh`, the click on the created webjob, click `run`, then click `logs` to see the output of `run.cmd` and `run.py`)

4. optional: setup the connection to Azure SQL database by following these steps, then:
	1. If you're using Django, then in the `settings.py` file, make sure you're information is like thi:
	   