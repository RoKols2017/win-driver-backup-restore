# Execution Policy в PowerShell

`Execution Policy` определяет, как PowerShell относится к запуску скриптов и файлов, скачанных из интернета.

## Как посмотреть текущие значения

```powershell
Get-ExecutionPolicy -List
```

## Рекомендуемый вариант

Для обычного локального использования удобен и достаточно безопасен вариант:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

Он позволяет запускать локальные скрипты, а для скачанных файлов требует корректный статус доверия.

## Разовый запуск без постоянного изменения policy

```powershell
powershell.exe -ExecutionPolicy Bypass -File .\backup-drivers.ps1
```

## Если скачанный файл заблокирован

```powershell
Unblock-File .\backup-drivers.ps1
```

При необходимости то же самое можно сделать и для второго скрипта:

```powershell
Unblock-File .\restore-drivers.ps1
```

## Предупреждение

Не используйте `Unrestricted` без реальной необходимости. Это ослабляет защиту и обычно не требуется для такого сценария.
