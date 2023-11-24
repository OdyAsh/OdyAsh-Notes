
# Bash Overview

[amazing source](https://towardsdatascience.com/bash-for-data-scientists-data-engineers-mlops-engineers-a8e389621e2e)

## What is Bash Programming?

- Bash is an acronym for “**_Bourne Again Shell,_**” developed in 1989.
- Data scientists use bash for preprocessing large datasets.
- Data Engineers need to know bash scripting for interacting with Linux and creating data pipelines, etc.
- Bash is used mostly in Linux and Mac OS. 
	- Windows uses a command prompt and power shell to perform the same operations. 
	- Now you can install bash in windows and perform the same operations as in Linux and Mac.

Regarding the relation between a Command Line Interface (CLI) and Bash:

![](Media-Temp/Pasted%20image%2020231124193625.png)

Note regarding the prompt interface:

![](Media-Temp/Pasted%20image%2020231124193939.png)

Types of shells:

![](Media-Temp/Pasted%20image%2020231124194030.png)

## Bash Syntax

![](Media-Temp/Pasted%20image%2020231124194158.png)

![](Media-Temp/Pasted%20image%2020231124194229.png)

![](Media-Temp/Pasted%20image%2020231124194320.png)

Note: PWD means parent working directory.

**Man command:**

Man command in Linux is used to display the user manual of any command that we can run on the terminal. It provides a detailed view of the command.

For example, `man ls` shows the below output - help for ls command.

![](Media-Temp/Pasted%20image%2020231124194440.png)

**Bash command Structure:**

`**command -options arguments**`

for example

`$ls (options) (file name or directory)`

`$ls -lah ~`

To check all the commands available in bash:

* find the directory for example **/usr/bin**  
* change to that directory `cd /usr/bin`
* then use the ls command `ls -la`

![](Media-Temp/Pasted%20image%2020231124194607.png)

Then it lists all the available commands:

![](Media-Temp/Pasted%20image%2020231124194615.png)

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

#Command:12
#copy a file
$ cp file1.txt file2.txt # file1 is copied to file2

#Command:13
#remove a file and remove a file directory
$ rm myfile.txt
$ rm -r mydirectory_name
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

# How to Run Linux

[source](<[amazing source](https://towardsdatascience.com/bash-for-data-scientists-data-engineers-mlops-engineers-a8e389621e2e)>)

If you don’t have a Linux machine then you can try the following:

![](Media-Temp/Pasted%20image%2020231124193731.png)

