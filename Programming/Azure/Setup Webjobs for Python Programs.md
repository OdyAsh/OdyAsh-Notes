Side note: if you have a student account (e.g., abcd@bue.edu.eg) then sign up to student services, if it says you're not eligible, then fill a support ticket with the issue [here](https://azure.microsoft.com/en-us/support/create-ticket/).

1. Create a web-app from here:
![[Pasted image 20230208145008.png|center|175]]
and make sure to choose any language (e.g., .NET) that supports windows o.s

2. follow [these](https://stackoverflow.com/questions/66426111/how-to-pip-install-extension-modules-in-azure-web-jobs) steps:
   ![[Pasted image 20230208154305.png | center | 300|450]]
   ![[Pasted image 20230208154359.png | center]]
   (don't forget to click "Restart Site" button on top-right corner of image above for the server to acknowledge the python extension)
   but instead of making a .bat file, make it `run.cmd`, and use the following code instead:
``` windows-cmd
C:\home\python364x64\python.exe -m pip install --upgrade -r requirements.txt
C:\home\python364x64\python.exe {relative-path-to-your-file}/run.py
```
Side-note: why this path for python.exe? Because I've found that python is installed there from here:
![[Pasted image 20230208154527.png | center | 250]]
Then, open the app service editor of your webapp:
![[Pasted image 20230211074828.png|center]]
then get the requirements.txt of your project and add it here:
![[Pasted image 20230211074523.png|center]]
3. Then follow these steps ([source](https://stackoverflow.com/questions/53850537/python-azure-webjob-import-error-cannot-import-python-extension-modules)): 
   open the cmd debug console from here:
   ![[Pasted image 20230211075242.png|center|375]]
   then here:
   ![[Pasted image 20230211075334.png|center]]
then, while in the python folder (i.e., `C:\home\python364x64>`), execute the following command:
``` windows-cmd
python.exe -m pip install --upgrade pip
python.exe -m pip install -r C:\home\site\wwwroot\requirements.txt
```
Then validate that the libraries are installed in `python364x64/Lib/site-packages` using this command (side-note: make sure you're still here: `C:\home\python364x64>`):
``` windows-cmd
python.exe -m pip list
```
4. create the webjob from here:
   ![[Pasted image 20230208151751.png | center | 600|500]]
   (where you'll add the webjob, press `referesh`, the click on the created webjob, click `run`, then click `logs` to see the output of `run.cmd` and `run.py`)
   
   Note: if you're unable to create webjob from Azure portal, then manually create a job like so:
   ![[Pasted image 20230211080253.png|center|525]]
   where `my_job_name` and `my_project` can be named however you want. Just make sure to right-click `my_project.zip` and press `Extract All`, and to adjust the CRON expression in `settings.job` to suit your needs. After that, go back to the webjob page in Azure portal and press `refresh`, you should see a new job with the name `my_job_name` 
   (side-note: if the schedule is written as `n/a`, then just run the job and click `refresh`, it will change to the CRON expression that you've written in `settings.job`)
   (another tricky side-note: in most cron expression websites, you'll see 5 fields only, but in azure webjobs, the expression consists of 6 fields --> ***second***, minute, hour, day, week, month)

5. optional: setup the connection to Azure SQL database by following these steps, then:
	1. Create Azure SQL database (if you have SQLite db with < 50k rows per table then check [this](https://www.dbsofts.com/articles/sqlite_to_azure/) then [this](https://stackoverflow.com/questions/44895079/convert-sqlite-database-to-db-file#:~:text=The%20name%20of%20your%20file%20is%20completely%20irrelevant%20to%20the%20data%20inside%20of%20it.%20Assuming%20the%20data%20structure%20is%20properly%20setup%2C%20simply%20renaming%20the%20file%20will%20suffice.), and if you have SQL server db, i.e., .bacpac file, then check [this](https://learn.microsoft.com/en-us/azure/azure-sql/database/database-import?view=azuresql&tabs=azure-powershell))
	2. If you're using Django, then in the `settings.py` file, make sure your information is like this:
![[Pasted image 20230211080701.png|center|425]]
	   where `NAME` is the name of the db as it appears in SSMS and `HOST` is also shown in the example below:
![[Pasted image 20230211080900.png|center|300]]
	   `USER` and `PASSWORD` are what you use to enter your server in SSMS
	   `PORT` can be checked in Azure, but it's probably `1433`