# Azure Pipelines Powershell Core

In this repository I present the options of running PowerShell Core in
Azure Pipelines with Windows hosts.

The reason I started looking into this is that PowerShell Core supports
UTF-8 by default.

I aimed to answer my own question in the
[Azure Pipelines tasks repository](https://github.com/Microsoft/azure-pipelines-tasks/issues/9496).

On non-Windows hosts I expect `powershell` and `pwsh` both run PowerShell Core,
but I was not sure if this was the case on Windows.

On Windows hosts, I found that:

- `task: PowerShell@2` with `pwsh: false` runs PowerShell
- `task: PowerShell@2` with `pwsh: true` runs PowerShell Core
- `powershell` runs PowerShell
- `pwsh` runs PowerShell Core

I determined this by checking the value of `$PSVersionTable.PSVersion`
returned by each shell.

You can see the example Azure pipeline in `azure-pipelines.yml`.

Version 5 is PowerShell which defaults to UTF-16.

Version 6 is PowerShell Core which defaults to UTF-8.

https://stackoverflow.com/a/40098904/2715716
