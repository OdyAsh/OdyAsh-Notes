
***TOC***:

1. [Windows Installation](#Windows%20Installation)
	1. [Install Node JS 18+](#Install%20Node%20JS%2018+)
	2. [Install WSL](#Install%20WSL)
		1. [On Windows](#On%20Windows)
		2. [And in VSCode](#And%20in%20VSCode)
	3. [Switch to a WSL Terminal](#Switch%20to%20a%20WSL%20Terminal)
	4. [Configure User Dir for Global Packages](#Configure%20User%20Dir%20for%20Global%20Packages)
	5. [](#)


# Windows Installation

The following is a quick guide on how to install [claude code](https://youtu.be/z37_rONQof8?t=191) for Windows.

Main sources:
* Medium article: [I tried Claude Code (3X Faster but Costly)](https://medium.com/ai-software-engineer/i-tried-claude-code-first-impression-install-and-start-using-it-1c96067a3163)

## Install Node JS 18+

Download Node JS version 18 or higher from [here](https://nodejs.org/en/download) (Just click `Windows Installer (.msi)` for a hassle-free experience).

Then, check that it works by running `node -v` and `npm -v` and getting back respective versions.

## Install WSL

### On Windows

In a terminal (e.g., PowerShell), execute: 
* `wsl --install`

Side note:
* Assuming you already have WSL installed with multiple distros, you can check them with:
	* `wsl --list --all`
* Then (optionally) change the default distro by running:
	* `wsl --setdefault <DistributionName>`
* So for example, if you set `Ubuntu` to the default distro, then when you activate the WSL terminal (will show how later), you will see a prefix like this in the terminal: 
	* `<USERNAME>@<LAPTOP-NAME>:/mnt/PATH/TO/PROJECT/Dir$`

### And in VSCode

* Install the [WSL VSCode extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl).


## Switch to a WSL Terminal

Now, whenever you want to run an application on WSL environment (e.g., claude code), then you'll first need to activate the WSL terminal. 

Since we currently want claude code to see our project that's open in VSCode, therefore we will:
* Open up a new terminal in VSCode, then execute this command:
	* `wsl`
* This will activate the terminal, and if `Ubuntu` is the current active distro, then you'll see the prefix previously mentioned (i.e., `<USERNAME>@...$`)
* Side note: Remember the password that you enter in the initial setup; you'll be prompted to enter it when doing certain operations in the WSL environment

## Configure User Dir for Global Packages

Now, inside the WSL terminal that you've just activated, execute these:

```bash
# Create a directory for global packages  
mkdir ~/.npm-global
# Configure npm to use the new directory  
npm config set prefix '~/.npm-global'
# Update your PATH (temporary for current session)  
export PATH=~/.npm-global/bin:$PATH
# Install Claude Code
npm install -g @anthropic-ai/claude-code
```

## Activate and Login

In the WSL terminal (obviously), run:
* `claude` 
to activate claude, then follow the login steps.

## Using an External API Key (Optional)

If you want to use someone else's API key instead of your own, then you'll jump through a few extra hoops. 

TL;DR: You have 2 methods.

Method 1 -> Update `.claude.json` file in home director (i.e., `~/`) (explanation resources: [~ , ls](https://www.perplexity.ai/search/briefly-explain-what-is-and-ls-M40eRPpUQKeFeJKuVcUTZw)):

* In the WSL terminal, run:
	* `ls -a ~` to see which files are in `~`.
* You should see a file called `.claude.json`. 
	* If not, run `claude`, then ask the LLM any question, then exit by tping `ctrl+c` twice, then check again, the file should now appear.
* Run `nano ~/.claude.json` to edit it;
	* Check for a key called `primaryApiKey`, change its value to the API key you want to use.
	* Then `ctrl+o`, `enter` to save the file. Then `ctrl+x` to exit `nano`.
* Close the current WSL terminal and open a new one for the effect to take place.
	* Side note: I think directly running `claude`  is sufficient, but I haven't tested this.
* Run `claude` and ask a question.
* Voila! You should now see it answering questions instead of saying `Credit balance too low`. 

Method 2 -> Create a Claude Config Dir per project:
* Suppose the current project that you want claude code to see has this path: `PATH/TO/PROJECT/DIR`.
* Then, in that path, create any folder (preferably, `.claude-config`), then in that folder, create a file called `config.json`.
* Then, in the WSL terminal, run this:
	* `export CLAUDE_CONFIG_DIR="$PWD/.claude-config"`
		* (Where PWD == Project Working Directory)
	* Then, run `claude`, and ask any question, then close it.
	* You should now find this `config.json` file populated with JSON code.
	* Look for `primaryApiKey`, change its value to the API key you want to use.
	* Repeat this process for each project dir. you want to work on.
	* Moreover, you'll need to run the `export ...` command above at the start of each WSL terminal session before running the `claude` command.

