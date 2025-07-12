
# Refreshing an Opened Terminal to Display New Environment Variables

Suppose you just installed a key like this:

![](Attachments%20-%20Powershell/Pasted%20image%2020250531144233.png)

![](Attachments%20-%20Powershell/Pasted%20image%2020250531144532.png)

Then, to make sure that the currently open terminal recognizes it, you need to refresh the terminal. You can do this by either:

1. Closing the terminal (or the IDE if you're running the terminal inside of one) and reopening it.
	1. Why?: Since in this command: `Get-ChildItem Env: | Sort-Object Name | Format-Table -AutoSize`, the `Env:` drive is populated when PowerShell starts and doesn't automatically refresh from registry changes.
	2. What's bizarre to me is that, if you're in an IDE, then opening a new terminal is not enough to refresh the environment variables; you have to close the IDE and reopen it.
	3. Side note: This is unlike running `[System.Environment]::GetEnvironmentVariables("Machine")` ( or `"User"` ), which will always fetch the latest environment variables from the registry.
2. Running the following PowerShell commands in the currently open terminal:
	1. (however, if you're in an IDE, then you have to do this each time you start a new terminal as well, until you decide to go with option 1)

```powershell

# For user-related environment variables, we pass `User`
foreach($var in [System.Environment]::GetEnvironmentVariables("User").GetEnumerator()) { Set-Item "env:$($var.Name)" $var.Value }

# For system-related environment variables, we pass `Machine`
foreach($var in [System.Environment]::GetEnvironmentVariables("Machine").GetEnumerator()) { Set-Item "env:$($var.Name)" $var.Value }
```

Then, display using this:

```powershell
Get-ChildItem Env: | Sort-Object Name | Format-Table -AutoSize
```

Sanity check: the outputs of the above command should yield the same key-value pairs you'd get if you run these 2 commands:

```powershell
# For displaying user-related environment variables currently in Windows' Registry
[System.Environment]::GetEnvironmentVariables("User").GetEnumerator() | Sort-Object Key | Format-Table -AutoSize

# For displaying system-related environment variables currently in Windows' Registry
[System.Environment]::GetEnvironmentVariables("Machine").GetEnumerator() | Sort-Object Key | Format-Table -AutoSize
```

# Changing Prompt Output

* Create a `.ps1` file in this path: `C:\Users\%USERNAME%\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1`
* Then, write code like this:

```powershell
function prompt {
    Write-Host "$($env:CONDA_PROMPT_MODIFIER)`n" -NoNewline -ForegroundColor Green
    Write-Host "$(Get-Location)`n" -NoNewline -ForegroundColor Cyan
    return "> "
}
```

Which will display content like this whenever opening Powershell in VSCode's terminal:

![](Attachments%20-%20Powershell/Pasted%20image%2020240511085625.png)

Note, check [this](https://code.visualstudio.com/docs/terminal/profiles#:~:text=Configure%20your%20default%20profile%20by%20running%20the%20Terminal%3A%20Select%20Default%20Profile%20command%2C%20which%20is%20also%20accessible%20via%20the%20new%20terminal%20dropdown) to make Powershell the default terminal in VSCode (in case you want to do this of course).

Pro-tip: if you later want to quickly see where that profile file is, do this in VSCode:

![](Attachments%20-%20Powershell/Pasted%20image%2020240518102903.png)
