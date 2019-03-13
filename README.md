# Azure Pipelines Powershell Core

In this repository I explore the options of running PowerShell Core in Azure Pipelines with Windows hosts.

The reason I started looking into this is that PowerShell Core supports UTF-8 by default.

I aimed to answer my own question here: https://github.com/Microsoft/azure-pipelines-tasks/issues/9496
In non-Windows hosts I expect `powershell` and `pwsh` both run PowerShell Core, but I was not sure if this was the case on Windows.

[
  ![](https://tomashubelbauer.visualstudio.com/azure-pipelines-powershell-core/_apis/build/status/azure-pipelines-powershell-core-CI?branchName=master)
](https://tomashubelbauer.visualstudio.com/azure-pipelines-powershell-core/_build/latest?definitionId=17&branchName=master)

The result of this investigation are as follows:

- `task: PowerShell@2` with `pwsh: false` runs PowerShell on Windows
- `task: PowerShell@2` with `pwsh: true` runs PowerShell Core on Windows
- `powershell` runs PowerShell on Windows
- `pwsh` runs PowerShell Core on Windows

I determined this by checking the value of `$PSVersionTable.PSVersion` returned by each shell.
Version 5 is PowerShell which defaults to UTF-16.
Version 6 is PowerShell Core which defaults to UTF-8.
https://stackoverflow.com/a/40098904/2715716
