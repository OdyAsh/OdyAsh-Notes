# VS Code Temporarily Freezes When Focusing on It

Possible fix: Make sure to hit the "collapse all" button here:

![Pasted image 20230304163503](../../Media/Default/Pasted%20image%2020230304163503.png)

# VS Code Makes Files Added To `.gitignore` Ready For `git commit`

Solution:
run the following command:
`git rm -r --cached folder_name`
This will remove the folder from the Git repository but will not delete it from your local file system. Here are the steps to do this:

Why does this happen? Answer (probably): 

If you have added a folder to `.gitignore` and committed the change to Git, then Git will ignore any changes made to that folder and will not track it. However, if you have already committed changes to the folder before adding it to `.gitignore`, then those changes will still be tracked by Git.

