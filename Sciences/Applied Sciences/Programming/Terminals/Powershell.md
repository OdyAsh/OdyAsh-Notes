
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

![](Media-Temp/Pasted%20image%2020240511085625.png)

Note, check [this](https://code.visualstudio.com/docs/terminal/profiles#:~:text=Configure%20your%20default%20profile%20by%20running%20the%20Terminal%3A%20Select%20Default%20Profile%20command%2C%20which%20is%20also%20accessible%20via%20the%20new%20terminal%20dropdown) to make Powershell the default terminal in VSCode (in case you want to do this of course).

Pro-tip: if you later want to quickly see where that profile file is, do this in VSCode:

![](Media-Temp/Pasted%20image%2020240518102903.png)
