[English](../en/execution-policy.md) | [Русский](execution-policy.md)

[Назад к README](../../README.ru.md)

# Execution Policy в PowerShell

`Execution Policy` определяет, как PowerShell относится к запуску скриптов, особенно скачанных из интернета.

## Как посмотреть текущие значения

```powershell
Get-ExecutionPolicy -List
```

## Рекомендуемый вариант

Для обычного локального использования рекомендуется:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

Этот режим позволяет запускать локальные скрипты и оставляет более безопасное поведение для скачанных файлов.

## Разовый запуск без постоянного изменения policy

```powershell
powershell.exe -ExecutionPolicy Bypass -File .\backup-drivers.ps1
```

## Снятие блокировки со скачанных файлов

```powershell
Unblock-File .\backup-drivers.ps1
Unblock-File .\restore-drivers.ps1
```

## Предупреждение

Не используйте `Unrestricted` без реальной необходимости.

## См. также

- [README.ru.md](../../README.ru.md) — обзор проекта и быстрый старт
- [README](../../README.md) — English landing page
