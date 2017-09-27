# Language Interop and .NET

## VER-01 Write for the lowest version of PowerShell that you can

As a rule, write for the lowest PowerShell version that you can, especially with scripts that you plan to share with others. Doing so provides the broadest compatibility for other folks.

That said, don't sacrifice functionality or performance just to stick with an older version. If you can safely write for a higher version (meaning you've deployed it everywhere the script will need to run), then take advantage of that version. Keep in mind that some newer features that seem like window dressing might actually have underlying performance benefits. For example, in PowerShell v3:

```PowerShell
Get-Service | Where-Object {$_.Status -eq 'Running'}
```

Will run significantly slower than:

```PowerShell
Get-Service | Where Status -eq Running
```

because of the way the two different syntaxes have to be processed under the hood.

**Further information**: You can get some detail on the differences between versions of PowerShell by typing `Get-Help about_Windows_PowerShell_5.0`.

## VER-02 Document the version of PowerShell the script was written for

All that said, make sure you specify the version of PowerShell you wrote for by using an appropriate `#Requires` statement:

```PowerShell
#Requires -Version 3.0
```

The `#Requires` statement will prevent the script from running on the wrong version of PowerShell.

### PowerShell Supported Version

When working in an environment where there are multiple versions of PowerShell make sure to specify the lowest version your script will support by providing a Requires statement at the top of the script.

```PowerShell
#Requires -Version 2.0
```

When a module uses specific cmdlets or syntax that is only present on a specific minimum version of PowerShell, specify this in the module manifest .psd1 file.

```PowerShell
PowerShellVersion = '3.0'
```
