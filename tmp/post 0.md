Basic Web-Scraping Project Setup
git vscode productivity webscraping
{%- # TOC start (generated with https://github.com/derlin/bitdowntoc) -%}

- [Introduction](#introduction)
- [Setting Up The Environment](#setting-up-the-environment)
  * [Setting Up GitHub Project From VSCode](#setting-up-github-project-from-vscode)
    + [Pulling & Pushing](#pulling-amp-pushing)
      - [Automate Pulling Changes from GitHub](#automate-pulling-changes-from-github)
      - [Committing & Pushing Changes to GitHub Using VSCode or Terminal](#committing-amp-pushing-changes-to-github-using-vscode-or-terminal)
  * [Setting Up a Virtual Environment `.conda`](#setting-up-a-virtual-environment-raw-conda-endraw-)
- [Wrap-Up 🙌](#wrapup)
- [Optional: Extra Content](#optional-extra-content)
  * ["Syncing" A Working File Across Devices Using VSCode](#syncing-a-working-file-across-devices-using-vscode)
  * [VSCode Shortcuts to Fold/Unfold Functions/Notebook Cells](#vscode-shortcuts-to-foldunfold-functionsnotebook-cells)
  * [dev.to Post Creation Tips: Creating TOC in dev.to, Spacing between Headers](#devto-post-creation-tips-creating-toc-in-devto-spacing-between-headers)

{%- # TOC end -%}

&nbsp;
## Introduction
Transitioning from "student" to "unemployed" came as a little shock for me and resulted in many hours of succumbing to movies/TV shows :].

THEREFORE, I've decided to get out of this rabbit hole by using [UpWork](https://www.upwork.com/) to get project ideas on what I love to do: _Web Scraping_.

(Side note: Even though I did the project on my own, you'll most likely see me use "we" instead of "I", because for some reason, using "I" makes me sound egotistic :].

&nbsp;
## Setting Up The Environment

Next, let's see how to use GitHub/Git/VSCode to properly set up a Python web-scraping project.

&nbsp;
### Setting Up GitHub Project From VSCode


These are the steps done to set up the project environment:

1. create a folder name for your project (e.g., reedsy-prompt-scraping).
2. open [VsCode](https://code.visualstudio.com/download).
3. `ctrl+k ctrl+o` and choose the folder that you've just created. (Side-note: this shortcut is read as: "press and **hold **ctrl, then press k, then press o).
4. `ctrl+shift+p` to open the command palette.
5. type `initialize` and choose `Git: Initialize Repository`.
6. follow these steps to create a folder/file:

    ![In VSCode: Create a folder called "secretss", and a file called .gitignore, both in the project's root directory. Then, in the .gitignore file, write `secretss/*` at the first line, then press ctrl+s to save the file (highlighted as (4) in the image)](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0zm1p5m1d7t9u2iy555n.png)
notice the white circle at (4)? This is because you didn't `ctrl+s` to save your .gitignore file! Always make sure you save please :]!

7. publish branch <a name="publish-branch-step">:

    ![In VSCode: Click on the source control tab found in the left pane, then write a commit message, then press the arrow-down button to the right of the commit button, then press "commit & sync"](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/j67l920yhit3notdo9mb.png)
and click `publish branch` then from the dropdown, choose either a private or a public repository.

&nbsp;
#### Pulling & Pushing

Now that you've got the project on GitHub, you can pull and push changes from/to GitHub. The sub-headers below explain how to do these commands.

&nbsp;
##### Automate Pulling Changes from GitHub

Using VSCode, you can lessen the possibility of [merge conflicts](https://www.datacamp.com/tutorial/how-to-resolve-merge-conflicts-in-git-tutorial) by following steps to automatically pull any changes from your project on GitHub to your local machine:

1. Install [Terminals Manager]:(https://marketplace.visualstudio.com/items?itemName=fabiospampinato.vscode-terminals) extension:   
 
    ![In VSCode: Click on extensions tab found in the left pane, then search for "Terminals Manager" extension and install the first one](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/t8r9m322qoe2k50skju8.png)

2. change default terminal to command prompt (cmd):

    ![using command palette](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lbjc3nq48613ik1fgr0d.png)

3. Create these files:

    ![creating .vscode folder, and inside it, create a file called terminals.json](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/j2ak6pbxqovtinyn8759.png)


to understand what's written in the `terminals.json` file, check out [this](https://marketplace.visualstudio.com/items?itemName=fabiospampinato.vscode-terminals#:~:text=%22autorun%22%3A%20true%2C%20//%20Execute,chest%22%2C%0A%20%20%20%20%20%20%20%20%22touch%20my_heart%22%0A%20%20%20%20%20%20%5D%2C) section in the extension's documentation.
here's the content in the `terminals.json` file:

```json
{
    "autorun": true,
    "autokill": true,
    "terminals": [
        {
            "name": "cmd (.conda)",
            "description": "To run '.conda' on startup",
            "open": true,
            "focus": false,
            "commands": [
                "where conda> nul 2>&1",
                "if %errorlevel% neq 0 (",
                "    echo condais not installed. Please install it from https://docs.conda.io/projects/miniconda/en/latest/miniconda-install.html",
                ") else (",
                "    conda.bat activate",
                "    condaactivate ./.conda",
                "    git pull",
                "    pip install -r requirements.txt",
                ")"
            ]
        }
    ]
}
```

Now, whenever you open this project, a command terminal will start and run the commands written in the list value of `commands` key in the code above. Additionally, the first command written there, which is `conda activate ./.conda` will activate the virtual environment that we'll set up in the upcoming section.

Side note: See [this](https://chat.openai.com/share/803cb244-bb66-4ebf-88cb-05ca1397bfec) ChatGPT chat to understand the commands above. In any case, If you don't want to automate this process, then comment the `git pull` line above, and to pull manually, you could either type `git pull` in the terminal, or you can just click here:

![Using source control tab of VSCode to pull new changes from GitHub](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/b1yno3q7z2yy496zg7we.png)

&nbsp;
##### Committing & Pushing Changes to GitHub Using VSCode or Terminal

To push changes, you can either use the terminal by executing [the following commands](https://chat.openai.com/share/20e21ac7-2314-422b-b679-818a921bde01):

```
git commit -a -m "test commit"
git push origin main
```

or you can use VSCode's interface, by following the steps shown in the image displayed below [publish branch](#publish-branch-step) step in the section above.

&nbsp;
### Setting Up a Virtual Environment `.conda`

Next, we'll be creating a virtual environment due [to its importance](https://chat.openai.com/share/403373ff-fe3f-4409-8729-5b404b250a91) in any Python project.

Follow these steps:

1. install anaconda from [here](https://docs.conda.io/projects/miniconda/en/latest/miniconda-install.html)

2. Run the following commands ([source](https://www.anaconda.com/blog/a-faster-conda-for-a-growing-community)):

    ``` cmd
conda update -n base conda
conda install -n base conda-libmamba-solver
conda config --set solver libmamba
```

3. `pip install` the suitable packages for our project. Obviously, we won't know all the required packages in advance, but we can start out with [these packages](https://chat.openai.com/share/615491bf-85d6-4122-b983-92473468ba35):

    ``` cmd
pip install ipykernel pandas helium line-profiler pip-chill py-heat-magic nbconvert beautifulsoup4 
```

4. type `create env` and choose the first option, then choose `conda`, then choose the suitable Python interpreter (suggestion: choose a version below 3.10, as 3.9x versions are [more compatible](https://www.reddit.com/r/Python/comments/qiyeqi/python_38_39_or_310_for_new_projects/?sort=new) with libraries).


    ![Command palette of VSCode](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/v9xslc5hqd0llzjilazt.png)


5. After the packages are installed, run this command in the terminal (cmd):
(Side-note: notice how now (.../.conda) should be visible in the terminal).

`(.../.conda) .../PATH/TO/PROJECT> pip-chill -v > requirements.txt`

this will only save [the packages that are not dependencies of installed packages](https://github.com/rbanffy/pip-chill#:~:text=only%20the%20packages%20that%20are%20not%20dependencies%20of%20installed%20packages) to a `requirements.txt` file in the project's root directory, which will be formatted like this:
(Side-note: you can also type `--no-version` in the command above if you don't want the versions to be mentioned).

```
...
pip-chill==1.0.3
py-heat-magic==0.0.2
testpath==0.6.0
toml==0.10.2
uri-template==1.3.0
webcolors==1.13
# anyio==4.0.0 # Installed as dependency for jupyter-server
# argon2-cffi==23.1.0 # Installed as dependency for jupyter-server
# argon2-cffi-bindings==21.2.0 # Installed as dependency for argon2-cffi
# arrow==1.2.3 # Installed as dependency for isoduration
# asttokens==2.2.1 # Installed as dependency for stack-data
# async-lru==2.0.4 # Installed as dependency for jupyterlab
# attrs==23.1.0 # Installed as dependency for jsonschema, referencing
# babel==2.12.1 # Installed as dependency for jupyterlab-server
# backcall==0.2.0 # Installed as dependency for ipython
# beautifulsoup4==4.12.2 # Installed as dependency for nbconvert
...
```

&nbsp;
## Wrap-Up 🙌

Hope you learned a thing or two from the basic setup steps mentioned here :]!

In this series' upcoming post, we'll actually talk about the code responsible for scraping [reedsy.com](https://reedsy.com/)!

If you have any questions/suggestions, don't hesitate to write them in the comment section; this is my first, post on Dev.to, so I still have [a lot to learn](https://dev.to/francescoxx/an-article-to-help-you-to-write-your-first-article-1mgm)! :]🙌!

&nbsp;
## Optional: Extra Content
Mostly unrelated info that I've learned along the way and that might come in handy for other projects :]🙌!

Side-note: If you check this post later and find some of these sub-headers removed, then I've probably created a newer post talking specifically about these removed topics.

&nbsp;
### "Syncing" A Working File Across Devices Using VSCode

Suppose you're coding in a file called `scrape.ipynb`, on your [PC](https://www.memedroid.com/memes/detail/3982173/Gamers-now-vs-then?refGallery=tags&page=1&tag=pc+gaming), and suddenly you need to work on that file remotely (i.e., on your [laptop](https://www.memedroid.com/memes/detail/3887312/Laptops-that-never-sleep?refGallery=tags&page=1&tag=laptop)), how do you proceed? Three options:

1. send the file using good ol' WhatsApp web.
2. send the file using a good ol' USB.
3. push the file to GitHub repo, then pull it on your laptop.
4. use VSCode's "[Cloud Changes](https://pawelgrzybek.com/use-cloud-changes-in-vs-code-to-sync-uncommitted-edits-between-two-computers/#:~:text=Enable%20the%20feature%20on%20both,it%20under%20accounts%20settings%20UI.)" feature (also called "[Edit Sessions](https://code.visualstudio.com/updates/v1_74#_improvements-to-continue-working-on)") to store/resume working changes (i.e., `scrape.ipynb` file and any other files that you have modified).

Options 1 and 2 are too primitive, while option 3 could be a hassle if you want your commits to be a complete logical update in the code. Therefore, let's introduce option 4: Using VSCode to sync files :]!

Follow these steps:

1. In your primary device (in our example, PC):
1.1 `ctrl+shift+p`
1.2 type `cloud`, then choose the `Store Working Changes` option:

    
    ![Selecting "store working changes" from VSCode's command palette](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hqey09v8aaj78rlyfo41.png)

2. In your secondary device (in our example, laptop):
2.1 `ctrl+shift+p`
2.2 type `cloud`, then choose the `Resume Latest Changes` option:


    If a prompt appears saying that you'll lose current changes done to `scrape.ipynb`, accept it so long as you didn't make any useful changes in that file.


That's it! When you're done, you can push changes from your secondary device (i.e., laptop) onto GitHub, and then pull these changes to your PC.
(Side note: make sure to discard the changes that you've made on your PC, since they are now outdated, and in order to avoid merge conflicts).

&nbsp;
### VSCode Shortcuts to Fold/Unfold Functions/Notebook Cells

Follow these steps:

1. `ctrl+shift+p`
1. type `shortcuts` and choose `Preferences: Open Keyboard Shortcuts (JSON)`.
1. add the following code to the start of the list:

``` JSON
    {
        "key": "ctrl+shift+g", // note: make cursor on function name
        "command": "editor.foldRecursively",
        "when": "editorTextFocus && foldingEnabled"
    },
    {
        "key": "ctrl+shift+h",
        "command": "editor.unfoldRecursively",
        "when": "editorTextFocus && foldingEnabled"
    },
    {
        "key": "ctrl+shift+alt+g", // note: make cursor anywhere in a cell
        "command": "editor.foldAll",
        "when": "editorTextFocus && foldingEnabled"
    },
    {
        "key": "ctrl+shift+alt+h",
        "command": "editor.unfoldAll",
        "when": "editorTextFocus && foldingEnabled"
    },
 ```

Now, you can easily fold/unfold code for increased readability in your notebook file:

![folding/unfolding code in VSCode](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/c1ghh7tws6ef887vlqdj.gif)

Of course, feel free to change the shortcuts in the code above!

&nbsp;
### dev.to Post Creation Tips: Creating TOC in dev.to, Spacing between Headers

* [BitDownTOC](https://derlin.github.io/bitdowntoc/) was used to generate the table of contents (TOC) for this post. Also, check [this issue](https://github.com/derlin/bitdowntoc/issues/17) if you want :].

* you can type `&nbsp;` before each header (e.g., `#Introduction`) in order to leave space before it.
