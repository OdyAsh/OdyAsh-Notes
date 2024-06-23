
# DE Job Description Example

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231205212153.png)


# Bash Overview

[amazing source](https://towardsdatascience.com/bash-for-data-scientists-data-engineers-mlops-engineers-a8e389621e2e); please don't forget to like/share/comment in that TWD (towards data science) article if you find the content below useful.

## What is Bash Programming?

- Bash is an acronym for “**_Bourne Again Shell,_**” developed in 1989.
- Data scientists use bash for preprocessing large datasets.
- Data Engineers need to know bash scripting for interacting with Linux and creating data pipelines, etc.
- Bash is used mostly in Linux and Mac OS. 
	- Windows uses a command prompt and power shell to perform the same operations. 
	- Now you can install bash in windows and perform the same operations as in Linux and Mac.

Regarding the relation between a Command Line Interface (CLI) and Bash:

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231124193625.png)

Note regarding the prompt interface:

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231124193939.png)

Types of shells:

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231124194030.png)

## Bash Syntax

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231124194158.png)

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231124194229.png)

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231124194320.png)

Note: PWD means parent working directory.

**Man command:**

Man command in Linux is used to display the user manual of any command that we can run on the terminal. It provides a detailed view of the command.

For example, `man ls` shows the below output - help for ls command.

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231124194440.png)

**Bash command Structure:**

`**command -options arguments**`

for example

`$ls (options) (file name or directory)`

`$ls -lah ~`

To check all the commands available in bash:

* find the directory for example **/usr/bin**  
* change to that directory `cd /usr/bin`
* then use the ls command `ls -la`

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231124194607.png)

Then it lists all the available commands:

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231124194615.png)

You can use the `man` command to check the info.


## Important Commands

```bash
#Command:1
#To check the current working directory
$ pwd

#Command:2
#To check the files in the directory
$ ls directoryname
$ ls -a     # to display the hidden files in the dircetory
$ ls -r    # to display the files in the reverse order

#Command:3
#To check the documentation
$ man ls

#Command:4
#To check the number of lines, words, and characters in a file
$ wc myfile.txt

#Command:5
#head command prints the first lines of a file
$ head -n5 myfile.txt

#Command:6
#To print the column values
$ cut -f2 myfile.txt #print the 2nd column
$ cut -f2-4 myfile.txt #print columns 2 to 4

#Command:7
# To search a string and then print-use the grep command
# Stands for global regular expression print
$ grep python myfile.txt # prints the lines which contains python

#Command:8
# To sort the lines in a file
$ sort myfile.txt
$ sort -r myfile.txt # sort in descending order use -r

#Command:9
#To remove the duplicate entries in a file
$ uniq myfile.txt

#Command:10
#Change the current directory
$ cd \usr\bin # changes to the directory \usr\bin from the curr directory

#Command:11
#move or rename the file
$ mv file1.txt file2.txt
#you can also move a directory or multiple directories
$ mv d1 d2 d3 /tmp

#Command:12
#copy a file
$ cp file1.txt file2.txt # file1 is copied to file2
#you can also copy director(y)(ies), but here, we add -r to copy recursively
$ cp -r d1 d2 d3 /tmp

#Command:13
#remove a file and remove a file directory
$ rm myfile.txt
$ rm -r mydirectory_name
# will remove only empty directories:
$ rmdir dir1 dir2 dir3

#Command:14
#create a file directory
$ mkdir file_dir_name
$ mkdir dir_1 dir_2 dir_3   # multiple directories creation

#Command:15
#output the string or text to the screen or to a file
$ echo 'Hello World'
$ echo 'Hello World' > file.txt

#Command:16
#create a file
$ touch my_file.txt

#Command:17
#To concatenate, read and file creation use cat command
#Note: use tac command to read file from last line to first line
$ cat file1 file2 file3 > file4

#Command:18
#To see the previously used commands
$ history

#Command:19
#Clear the terminal screen
$ clear

#Command:20
#To reboot the system
$ reboot

#Command:21
#Find the differences betewen 2 files
$ diff my_file1.txt my_file2.txt

#Command:22
#add a user
$ useradd David

#Command:23
# to exit the terminal
$ exit

#Command:24
#kill – Kill a process by ID
#killall – Kill a process by name
$ kill -9 3827

#Command:25
#sleep comman to make the system idle
$ sleep 10  # sleeps for 10 seconds

#Command:26
#To check the space used and available on the currentfile systems
$ df

#Command:27
#check the file and directory sizes
$ du

#Command:28
#check the file information
$ file my_file.txt

#Command:29
# To get the information about the used and unused memory
$ free

#Command:30
# To compress or decompress the file
$ gzip -d file.gz
#To decompress a file -d

#Command:31
# stops all the CPU functions
$ halt

#Command:32
# To check the host name
$ hostname

#Command:33
# more command is used to view the text files in the command prompt
$ more my_file.txt

#Command:34
# Less is a command line utility that displays the contents of a file or a command output, one page at a time.
$ less my_file.txt

#Command:35
# To destroy a file use shred
$ shred file1.txt

#Command:36
# tar command used to archive files in tar format.
$ tar -cf my_files.tar ny_file1 my_file2

#Command:37
# call the Vim editor
$ vim my_file.txt

#Command:38
# To display the user logged in 
$ w

#Command:39
# To get a brief the description of the keyword
$ whatis grep
$ whatis keyword(s)
```


### Shell Piping

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231125035014.png)

A pipe connects the standard output of a command to the standard input of a command. There can be multiple pipes or a single pipe.

Example:

```bash
cat user_names.txt|sort|uniq
```

The `cat` standard output is passed as input to the sort and then the standard output of the `sort` is passed as input to the `uniq` command. All are connected by the pipe command. Visualization of the output:

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231125035445.png)

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231125035505.png)

You should use piping `|` if you want to pass outputs between programs; use redirection `>` or `>>` if you want to write to a file. ([source](https://stackoverflow.com/questions/9553628/piping-and-redirection#:~:text=You%20should%20use%20piping%20if%20you%20want%20to%20pass%20outputs%20between%20programs%3B%20use%20redirection%20if%20you%20want%20to%20write%20to%20a%20file))

### grep Command

- GREP stands for **“global regular expression print”**.Grep is used to search for specific patterns in a file or program output.
- Grep is a powerful command and is used heavily. Please check the below examples.

```bash
$ grep [option(s)] pattern [file(s)]
​
#Search any line that contains the word 
$ grep 'word' filename

#Look for all files in the current directory and in all of its subdirectories 
$ grep -R 'Error' ​

#egrep is internally "grep -E", which enables usage of extended regexp patterns.
#This allows use of meta-symbols such as `+`, `?` or `|`.
#So if we use grep here instead, it will search for "Male|Doctorate" instead
#of searching for the word "Male" or the word "Doctorate"
#More info: https://stackoverflow.com/a/18076933
$ egrep -w 'Male|Doctorate' adult_t.csv

#search for the whole word
$ grep -w "Masters" adult_t.csv
​
#Perform a case-insensitive search for the word ‘doctorate’ 
$ grep -i 'doctorate' adult_t.csv
​
#Search and display the total number of times that the string ‘doctorate’ appears in a file adult_t.csv:
$ grep -c 'Doctorate' adult_t.csv
​
#search for a word in more than one file
$ grep California f1.txt f2.txt f3.txt
```

### sed Command

`grep` vs `sed` ([source](https://www.fosslinux.com/103848/searching-and-manipulating-text-with-grep-and-sed.htm#:~:text=Conclusion,used%20to%20edit%20text%20files.)):
* `grep` can be used to search for patterns in a file or input.
* `sed` can be used to edit text files.

Practical examples of `sed` command can be found [here](https://linuxhint.com/50_sed_command_examples/). Few examples:

```bash
echo "Bash Scripting Language Bash" | sed 's/Bash/Perl/g'
# output: Perl Scripting Language Perl
# "s/" replaces first string with second string
# "/g" matches all strings, instead of just the first one, 
# so if it was omitted, then output will be: "Perl Scripting Language Bash"
```

### curl Command

* `curl` is a tool for transferring data from or to a server. 
* It stands for "Client URL"
* It supports these protocols: DICT, FILE, FTP, FTPS, GOPHER, GOPHERS, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, MQTT, POP3, POP3S, RTMP, RTMPS, RTSP, SCP, SFTP, SMB, SMBS, SMTP, SMTPS, TELNET or TFTP.

```bash
curl [options / URLs]

#Examples (source: https://devhints.io/curl)
# Post data:
curl -d password=x http://x.com/y
# Auth/data:
curl -u user:pass -d status="Hello" http://twitter.com/statuses/update.xml
```

### Bash Variables

- In bash, you don’t have to declare the type of the variable like string or integer, etc. 
	- It is similar to python.
- **Local variables** are declared at the command prompt. 
	- It is available only in the current shell. 
	- They are not accessible by child processes or programs. 
	- All user-defined variables are local variables.
- The `export` command is used to create the **environment variable**. Environment variables are available to child processes.
- There should not be any space when you assign the value.
	- E.g., `my_ev='Tesla'`, not `my_ev = 'Tesla'`
- It is best practice to use lowercase to declare local variables and uppercase to declare environment variables.

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231125040157.png)

### Root Privileges and sudo Command

Regarding `sudo` ([source](https://phoenixnap.com/kb/linux-sudo-command#:~:text=Sudo%20stands%20for%20SuperUser%20DO,sensitive%20files%20from%20being%20compromised.)):
* Sudo stands for **SuperUser DO** and is used to access restricted files and operations. 
* By default, Linux restricts access to certain parts of the system preventing sensitive files from being compromised.
* The `sudo` command temporarily elevates privileges allowing users to complete sensitive tasks without logging in as the root user.
* When the `sudo` command is used, a timestamp is entered in the system logs. 
	* The user can run commands with elevated privileges for a short time (default 15 minutes). 
	* If a non-sudo user tries to use the `sudo` command, it is logged as a security event.
* By default, a single-user system grants `sudo` privileges to its user. 
	* A system or server with multiple user accounts may exclude some users from `sudo` privileges.
	* In Debian/Ubuntu, the `sudo` group controls `sudo` users. Add a user to the `sudo` group with the following command: `usermod -aG sudo [username]`


### Packaging Systems

What is apt-get?:
- `apt-get` (Advanced Package Tool) is a friendly command-line tool to interact with the packaging system.
- Some popular package managers include **apt, Pacman, yum, and portage.**

Some important commands:

```bash
# Updating the package database 
$ sudo apt-get update

# Once you have updated the package database, you can upgrade the installed packages
$ sudo apt-get upgrade

# To upgrade only a specific package
$ sudo apt-get upgrade <package_name>

# Search for a package
$ apt-cache search <search term>

# install a package
$ sudo apt-get install <package_name>

# install multiple packages
$ sudo apt-get install <package_1> <package_2> <package_3>

# install a package and no upgrade
$ sudo apt-get install <package_name> --no-upgrade

# Remove a package
$ sudo apt-get remove <package_name>

# remove a package using purge
$ sudo apt-get purge <package_name>
```

### &, &&, |, || Operators

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231125041203.png)

Example:

```bash
cd my_dir && pwd || echo “No such directory exists”
```

* If the `my_dir` exists, 
	* then the current working directory is printed 
		* (as `pwd` stands for "print working directory", [source](<https://unix.stackexchange.com/questions/709896/what-is-the-difference-between-cwd-and-pwd#:~:text=cwd%3A%20current%20working,directory%20(a%20command)>)). 
* If the `my_dir` doesn’t exist, 
	* then the message "No such directory exists" is printed.

## Find and Locate

- The find command is used to find files or directories in real-time. It is slow compared to Locate.
- It searches for a pattern in the current directory.

Syntax:

```bash
find [path...] [expression]​
#f: a regular file
#d: directory
#l: symbolic link
#c: character devices
#b: block devices
#p: named pipe (FIFO)
#s: socket

```

Examples:

```bash
#Find by name
$ find . -name "my_file.csv"
#Wildcard search
$ find . -name "*.jpg"
#Find all the files in a folder
$ find /temp
#Search only files
$ find /temp -type f
#Search only directories
$ find /temp -type d
#Find file modified in last 3 hours
$ find . -mmin -180
#Find files modified in last 2 days
$ find . -mtime -2
#Find files not modified in last 2 days
$ find . -mtime +2
#Find the file by size
$ find -type f -size +10M
```

- Locate is: 
	- much faster
	- not real-time, but scans in a pre-build database.
	- used to find the locations of files and directories.
- If locate command is not available then you need to install it before using it. Check your Linux distribution and install it

```bash
$ sudo apt update          # Ubuntu
$ sudo apt install mlocate # Debian
```

The database has to be updated manually using `updatedb`  before using the Locate command. The database update happens every day using an internal cron expression ([source](https://linuxize.com/post/locate-command-in-linux/)):

```bash
$ sudo updatedb
```

### Split a File

If you have a large file then you might have a requirement to split the larger file into smaller chunks. For splitting the file, you can use:

```bash
#Running the split command without any options will split a file into 1 or more separate files containing up to 1000 lines each.The files created with names xaa, xab, xac, etc.
$ split my_file
​
#To change the prefix, add your desired prefix to the end of the command line
$ split my_file my_prefix
​
# the default split is 1000 lines. if you want to use a custom one, then use the below.
$ split --lines=5000 my_file
​
#Also you can specify the file size
$ split --bytes=10 MB my_file
```

## File Management

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231125041902.png)

```bash
ls [option] file_name

#To view the hidden files
ls -a

#To view the files in reverse order
ls -r

#To display the last 10 recently modified files. 
ls -lt | head -n5
#l - long listing format, 
#t - sorted by time, 
#head - select the first 5 records.

#To display the files sorted by file size.
ls -l -S
```

Most `ls` options:

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231125042406.png)

## Data Science Related Commands

### CSV Related Commands

[csvkit](<[csvkit](https://csvkit.readthedocs.io/en/latest/)>) is a suite of command-line tools for converting to and working with CSV.

Install csvkit from [here](https://csvkit.readthedocs.io/en/latest/tutorial/1_getting_started.html). In short, run this: `sudo pip install csvkit`

Some commands:

```bash
# To check the names of the columns
csvcut -n adult_t.csv
# To check only a few columns
csvcut -c 2,5,6 adult_t.csv
#To check by column names
csvcut -c Workclass,Race,Sex adult_t.csv
# You can use the pipe command and check the first few rows of the selected columns
csvcut -c Age,Race,Sex adult_t.csv | csvlook | head

# Here I want to select all the candidates who have doctorates, and a husband and race are White
grep -i "Doctorate" adult_t.csv | grep -i "Husband" | grep -i "Black" | csvlook

# To find the statistics use the csvstat
csvcut -c Age,Education,Hours/Week adult_t.csv | csvstat

#To merge 2 files. You can use the csvjoin
#Note: 'cf' is the common column between the 2 files.
csvjoin -c cf data1.csv data2.csv > joined.csv

#Note: querying from the CSV file is slow when compared to querying from the SQL table. The entire CSV file is loaded in the in-memory and if the dataset is large then it will affect the performance.
#More info: https://csvkit.readthedocs.io/en/latest/tutorial/3_power_tools.html#csvsql-and-sql2csv-ultimate-power
csvsql --query "select county,item_name from a_table where quantity > 5;" a_table.csv | csvlook

#Find the difference between 2 files
#Example: If you want to find the customers who are available in the file and not in file 2 then use diff file1 file2. The output will display all the customer's Id’s which are not available in file2.
#options
#a : add
#c : change
#d : delete
diff [options] File1 File2

#AWK Stands for: Aho, Weinberger, Kernighan (authors)
#AWK is a scripting language and is used for text processing.
#AWK programs are made of one or many `pattern { action }` statements.
#AWK tutorial with examples: https://linuxhandbook.com/awk-command-tutorial/
#If you want to print columns 1 and 2 and the first few records:
awk -F, '{print $1,$2}' adult_t.csv | head
#Find out the no of hours/ week > 98:
awk -F, '$13 > 98' adult_t.csv | head
#To print all lines:
awk '1 { print }' adult_t.csv

```



# How to Run Linux

[source](<[amazing source](https://towardsdatascience.com/bash-for-data-scientists-data-engineers-mlops-engineers-a8e389621e2e)>)

If you don’t have a Linux machine then you can try the following:

![](Attachments%20-%20DE%20Road%20Map/Pasted%20image%2020231124193731.png)

