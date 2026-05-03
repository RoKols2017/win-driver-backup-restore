[English](execution-policy.md) | [Русский](../ru/execution-policy.md)

[Back to README](../../README.md)

# Execution Policy in PowerShell

`Execution Policy` controls how PowerShell handles script execution, especially for files downloaded from the internet.

## Check Current Policies

```powershell
Get-ExecutionPolicy -List
```

## Recommended Setting

For normal local use, this is the recommended option:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

It allows local scripts to run and keeps a safer default for downloaded files.

## One-Time Run Without Permanent Change

```powershell
powershell.exe -ExecutionPolicy Bypass -File .\backup-drivers.ps1
```

## Unblock Downloaded Files

```powershell
Unblock-File .\backup-drivers.ps1
Unblock-File .\restore-drivers.ps1
```

## Warning

Do not use `Unrestricted` unless you have a specific reason to do so.

## See Also

- [README](../../README.md) — project overview and quick start
- [README.ru.md](../../README.ru.md) — Russian landing page
