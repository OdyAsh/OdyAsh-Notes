# Git Basics

[source 1](https://www.youtube.com/watch?v=8JJ101D3knE), [source 2](https://tammy.ai/e/oBvRi1NShMVo6?type=pro)

- Git is a distributed version control system where each team member has a [copy](https://youtu.be/8JJ101D3knE?t=91) of the project with its history on their machine.
- configurations settings like name, email, default editor, line ending, can be specified at three different levels ([7:30](https://youtu.be/8JJ101D3knE?t=474)): SYSTEM, GLOBAL, LOCAL:
  
  ![](Media-Temp/Pasted%20image%2020240119175432.png)
  
- Check out [this](https://stackoverflow.com/questions/68975299/why-should-i-use-wait-when-selecting-my-default-editor-in-git#:~:text=your%2Dfile.extension%3E-,When%20you%20use,-code%20%3Cyour%2Dfile) SO answer to understand this command: `git config --global core.editor "code --wait"`
- to open configuration settings via editor: `git config --global -e`
- CR vs LF (11:00):
  
  ![](Media-Temp/Pasted%20image%2020240119181119.png)
  
- Therefore, Git manages this like so:
  
  ![](Media-Temp/Pasted%20image%2020240119181205.png)
  
- So, we run `git config --global core.autocrlf TYPE` where `TYPE = true (windows), TYPE = input (mac/linux)`.
- The "staging area" allows for reviewing and selecting changes to be included in the next commit.
- <mark style="background: #FFF3A3A6;">"Tracking a file" means adding it to the "staging area" (which was previously called "index").</mark>
	- However, <mark style="background: #D2B3FFA6;">there are other cases where a file can be considered "tracked"</mark>; check [this](https://iq.opengenus.org/file-stages-in-git/) article and [this](https://stackoverflow.com/questions/7564841/concept-of-git-tracking-and-git-staging) SO answer for details, but in summary, the files that are considered "tracked" files are either:
		- Staged, which are files that we've marked to be added to our next commit snapshot.
		- Committed (i.e., unchanged/unmodified), which are files that have not changed since its last commit.... If you modify them, they become:
		- Modified (i.e., unstaged), which are files that we've added changes to.
- Git's "staging area" is actually similar to a staging environment we use when releasing software to production ([19:00](https://youtu.be/8JJ101D3knE?t=1121)); It's either a reflection of what we currently have in production, or the next version that's going to go into production. This is why contrary to popular belief, <mark style="background: #FF5582A6;">the staged files aren't actually removed when performing a commit; they are simply stored and now reflect a snapshot of what we have in production (i.e., what got committed).</mark>
- <mark style="background: #FFB8EBA6;">Commits in git store complete snapshots of the project, not just the changes.</mark>
- Git is efficient in data storage by compressing file contents and avoiding duplicate content.
- Be cautious when using `git add .` command as it adds all files recursively.
- <mark style="background: #FFB8EBA6;">Modified files appear in the working directory and need to be added again to the staging area.</mark>
- In the screenshot below, the "3 insertions" refer to the two and one lines added to file1 and file2 respectively (27:00):
  
  ![](Media-Temp/Pasted%20image%2020240119182535.png)
  
- `echo hellooo > file1.txt` will overwrite content in `file1.txt` with `helooo`, while `>>` will append it.
- `rm` vs `git rm`
	- The former removes a file from both the current working directory only, while the latter removes it from the staging area as well.
	- same logic with `mv` vs `git mv` for moving (or renaming) a file.
- `git ls-files` tells us the files that are being tracked (i.e., in the staging area).
- <mark style="background: #D2B3FFA6;">If you track a file (i.e., add it to the staging area), then add this file to ".gitignore", it will not be ignored</mark>; you have to first remove it from the staging area using `git rm --cached -r bin/` if we want to recursively remove content inside `bin/` directory from the staging area ([40:00](https://youtu.be/8JJ101D3knE?t=2407)).


## Quickly Display Git Status

Example of `git status` ([43:00](https://youtu.be/8JJ101D3knE?t=2603)):

![](Media-Temp/Pasted%20image%2020240119212159.png)

This is too wordy, to shorten the output, write `git status -s`. Now, to understand the shortened output, consider these case scenarios:

You modify an existing file without staging it:

![](Media-Temp/Pasted%20image%2020240119212424.png)

You add it to the staging area:

![](Media-Temp/Pasted%20image%2020240119212501.png)

You modify it again:

![](Media-Temp/Pasted%20image%2020240119212519.png)

You stage it one last time:

![](Media-Temp/Pasted%20image%2020240119212543.png)

Now, you create a new file `file2.js`, then:

![](Media-Temp/Pasted%20image%2020240119212614.png)

Then, you decide to stage it:

![](Media-Temp/Pasted%20image%2020240119212640.png)

## Comparing The Changed Lines of Code

Suppose you previously committed `file1.js`, and you want to <mark style="background: #FFF3A3A6;">compare this old committed file with a modified staged file</mark> `file1.js` (i.e., that is currently in the staging area). Then:

`git diff --staged`. Now, assuming:

```js
// old-committed file1.js (which git refers to as a/file1.js)
hello
world
test
```

and:

```js
// new-staged file1.js (which git refers to as b/file1.js)
hello
world
test
sky
ocean
```

Then the output by the git command above:

![](Media-Temp/Pasted%20image%2020240119213540.png)

Where `1,3` means "starting from line 1, we extracted 3 lines (hello, world, test lines)", and the `-` sign means this extraction happened from `a/file1.js`.

By the same logic, `1,5` means "starting from line 1, we extracted 5 lines (hello, world, test, sky, ocean)", and the `+` sign means this extraction happened from `b/file1.js`.

Now, suppose we want to do the same for `file2.js`, but this time, the file wasn't previously committed. Therefore, the output will be:

![](Media-Temp/Pasted%20image%2020240119213906.png)

Now, we can write `git diff` (i.e., remove `--staged`) for the same logic above, but for <mark style="background: #FFF3A3A6;">comparing a file that is in the staging area, with a newer file that is in the current working directory</mark>. Note, in this case, the `a/file1.js` and `b/file1.js` is Git's way of referring to the staged file and the current directory file respectively.

Therefore, one can deduce that `a/file` and `b/file` <mark style="background: #FFB86CA6;">refer to an older file and a newer file respectively.</mark>

## Configuring VSCode as Default Diff Tools

First, run this command ([51:00](https://youtu.be/8JJ101D3knE?t=3054)):

![](Media-Temp/Pasted%20image%2020240119214743.png)

Then:

![](Media-Temp/Pasted%20image%2020240119214758.png)

Then:

![](Media-Temp/Pasted%20image%2020240119214847.png)


## Viewing Commit History

Type this ([57:00](https://youtu.be/8JJ101D3knE?t=3412)): `git log --oneline`:

![](Media-Temp/Pasted%20image%2020240119215212.png)

## Viewing a Commit

Using `git show [COMMIT|HEAD]`:

![](Media-Temp/Pasted%20image%2020240119215606.png)

![](Media-Temp/Pasted%20image%2020240119215652.png)

But this shows us what was changed, but what if we want to see the full file in that commit?: To do so, type this: `git show [COMMIT|HEAD]:RELATIVE_FILE_PATH`:

![](Media-Temp/Pasted%20image%2020240119215748.png)

The command above is for <mark style="background: #FFF3A3A6;">displaying a specific file in a specific commit</mark>, but what if we want to <mark style="background: #FFF3A3A6;">display all files in a specific commit?</mark>: To do so, use: `git ls-tree [COMMIT|HEAD]`:

![](Media-Temp/Pasted%20image%2020240119220117.png)

<mark style="background: #FFB86CA6;">So using the show command, we can view an object in the git database</mark>, where objects can consist of:

![](Media-Temp/Pasted%20image%2020240119220203.png)

## Unstaging Files

To unstage files, use `git restore --staged YOUR_FILE` where:
* `YOUR_FILE` can be one or more (space-separated) relative file paths (which contain wild cards), or simply, `.` to recursively restore all files.
* `--staged` means that `git restore` will <mark style="background: #FFB86CA6;">take a copy from the next environment and paste (or overwrite) it in the current environment.</mark> So since we passed `--staged`, the next environment will be the previous commit, and the current environment will be the staged area.
* If we didn't add `--staged`, then `git restore` will take a copy from the staged area, and paste (or overwrite) it in the current working directory.

Example:

![](Media-Temp/Pasted%20image%2020240119221141.png)

Why the output above?: As the `file1.js` file in the staged area is now identical to the previously committed `file1.js`, so git doesn't see modifications in the staged area related to `file1.js` anymore.

Another example:

![](Media-Temp/Pasted%20image%2020240119221321.png)

Why?: Since `file2.js` didn't previously exist in a previous commit (as can be deduced by seeing the `A` symbol), therefore, to restore it, git completely removes it from the staged area, so it is now stored in the current working directory only (which can be deduced by the `??`).

## Discarding Local Changes

To discard local changes (i.e., changes done in the current working directory, not the staging area), we also use the `git restore`, but without the `--staged` flag. 

For removing any modification/deletion done on all previously tracked files that are in the current working directory, we run: `git restore .`:

![](Media-Temp/Pasted%20image%2020240119223215.png)

For removing untracked files (i.e., files that were created for the first time and weren't previously staged/committed), we use `git clean -fd`, where `f` means `force`, and `d` means `remove whole directories`:

![](Media-Temp/Pasted%20image%2020240119223306.png)

## Restore a File to a Previous Version

Previously, we said that git restores a file from the next environment to the current one, but what if we don't want the "next environment", but an environment of our choosing?: Then, use the `--source` flag like so: `git restore --source=HEAD~1 file1.js`:

![](Media-Temp/Pasted%20image%2020240119223744.png)
## Infographics

[Amazing source 1 for infographics](https://blog.amigoscode.com/p/how-git-works?ref=dailydev)

![](Media-Temp/Pasted%20image%2020240118143700.png)

![git-commands-visualized](Media-Temp/git-commands-visualized.gif)

# Git Advanced Topics

## Git Pickaxe

[The git pickaxe](https://git-scm.com/docs/gitdiffcore#_diffcore_pickaxe_for_detecting_addition_deletion_of_specified_string) is an advanced feature for those very annoying (and hopefully rare) scenarios of source control; It digs through the entire commit history for a string (or regex pattern), returning all matching commit hashes ([source](https://medium.com/rightpoint/secrets-of-git-git-gotchas-tips-tricks-82a1df9fcc5d#:~:text=is%20an%20advanced%20feature%20for%20those%20very%20annoying)).

`$ git log -p -S "the thing you want to find"`

This allows you to find a change in your codebase without knowing when (or even where) it occurred:

```bash
$ git log -p -S "const password = 'N0tMyR3alP4ssword!"
commit 41658be12110473f85014dc47c7d691758407213
Author: hopefully_not_you <an@email.com>
Date: ...the rest of the commit, including a diff of the file
```

## Bash Function

Example of a bash function written in `.bash_profile` ([source](https://medium.com/rightpoint/secrets-of-git-git-gotchas-tips-tricks-82a1df9fcc5d#:~:text=A%20bash%20function%20would%20be%20perfect%20for%20this%20kind%20of%20scenario.%20Add%20the%20following%20to%20your%20bash_profile)):

```bash
# $/.bash_profile  
createEmptyBranch() {  
git checkout master && \  
git pull && \  
git branch $1 && \  
git checkout $1 && \  
git commit -m 'starting work' --allow-empty && \  
git push --set-upstream origin $1  
}
```

And now in a fresh terminal the following function should be available to you:

```bash
$ createEmptyBranch my-test-branch  
Switched to branch 'master'  
Your branch is up to date with 'origin/master'.  
Already up to date.  
Switched to branch 'my-test-branch'  
[my-test-branch f58c0e6] starting work  
Enumerating objects: 1, done.  
...  
* [new branch] my-test-branch -> my-test-branch  
Branch 'my-test-branch' set up to track remote branch 'my-test-branch' from 'origin'.
```

