
# Debugging Tips

## "Can't read" Error
If MySQL crashes while working, you'll likely find an error that MySQL can't read current schemas, solution (source, can't find it because I can't remember the exact error log...): delete content inside this path:

`C:\Users\YOUR-USERNAME\AppData\Roaming\MySQL\Workbench\sql_workspaces`


## Windows/MySQL Crashes When Running Queries

Solution 1 (preferable): Just install MySQL on a docker container. Steps:
* Install [docker desktop](https://www.docker.com/products/docker-desktop/)
* Install [MySQL installer](https://dev.mysql.com/downloads/installer/)
	* Choose `custom`
	* Install only `MySQL Workbench`, and choose version `8.0.20`, or any other version, but it should be compatible with the docker image that you'll pull (as seen below)
* open your terminal (CMD)
* type the following command ([source](https://hub.docker.com/_/mysql#:~:text=Starting%20a%20MySQL%20instance%20is%20simple%3A), which I found from [this](https://www.youtube.com/watch?v=kphq2TsVRIs) video): `docker run --name mysql-image-for-metabase -p 3306:3306 -e MYSQL_ROOT_PASSWORD=your_password_here -d mysql:8.0.20`
	* Note 1: the port doesn't have to be `3306`, it's just a convention in MySQL.
	* Note 2: you don't have to set the version to `8.0.20`, but you should choose the same version as 
* Open up `MySQL Workbench` and create a new connection:
  
  ![](Media-Temp/Pasted%20image%2020231107143803.png)
  
  Then click `test connection` button (at the bottom-right), and enter the same password used in the docker command that you executed in the above step.
* Congratulations, you can now use `MySQL Workbench` as an IDE to access your database which is inside a docker container.

Solution 2 ([source](https://stackoverflow.com/questions/63362585/mysql-crash-while-generating-entity-data-model-in-visual-studio-2019), which I found from [here](https://dba.stackexchange.com/a/291719)) (didn't work for me though):

In a new query tab, run this query (make sure you're logged in as an admin (i.e., someone with high privilege)):

````sql
Set global optimizer_switch='derived_merge=off,subquery_to_derived=off,prefer_ordering_index=off,semijoin=off';
````


Solution 3 (I don't know if this will work): make sure that you install a more stable (i.e., older) version across all MySQL components (after clicking `custom install` in MySQL installer of course).
