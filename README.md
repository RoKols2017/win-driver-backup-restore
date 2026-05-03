# win-driver-backup-restore

Минимальная PowerShell-утилита для резервного копирования и восстановления драйверов Windows 11 штатными средствами Windows.

## Для кого это

- Для пользователей Windows 11 перед переустановкой системы.
- Для тех, кто хочет сохранить установленные драйверы без сторонних программ.
- Для случаев, когда нужно быстро вернуть драйверы после чистой установки Windows.

## Что делает

- Экспортирует установленные сторонние драйверы через `Export-WindowsDriver`.
- Сохраняет драйверы в папку `C:\DriverBackups\<COMPUTERNAME>\<timestamp>\drivers`.
- Дополнительно сохраняет метаданные: список устройств, версии драйверов, сведения о системе и SHA256-хэши.
- Восстанавливает драйверы из конкретной папки `drivers` через `pnputil`.

## Скачать скрипты

Raw-ссылки:

- `https://raw.githubusercontent.com/RoKols2017/win-driver-backup-restore/main/scripts/backup-drivers.ps1`
- `https://raw.githubusercontent.com/RoKols2017/win-driver-backup-restore/main/scripts/restore-drivers.ps1`

Если вы публикуете fork в другом аккаунте, замените `RoKols2017` на имя своего GitHub-аккаунта.

Скачать через PowerShell:

```powershell
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/RoKols2017/win-driver-backup-restore/main/scripts/backup-drivers.ps1" -OutFile ".\backup-drivers.ps1"
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/RoKols2017/win-driver-backup-restore/main/scripts/restore-drivers.ps1" -OutFile ".\restore-drivers.ps1"
```

После скачивания может понадобиться снять блокировку:

```powershell
Unblock-File .\backup-drivers.ps1
Unblock-File .\restore-drivers.ps1
```

## Быстрый старт

1. Разрешить запуск скриптов для текущего пользователя:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

2. Запустить резервное копирование:

```powershell
.\backup-drivers.ps1
```

3. После переустановки Windows запустить восстановление:

```powershell
.\restore-drivers.ps1 -DriversRoot "C:\DriverBackups\HOSTNAME\YYYY-MM-DD_HH-mm\drivers"
```

Скрипты нужно запускать из PowerShell от имени администратора.

## Execution Policy

Проверить текущие политики:

```powershell
Get-ExecutionPolicy -List
```

Рекомендуемый вариант для обычного использования:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

Если файл скачан из интернета и заблокирован:

```powershell
Unblock-File .\backup-drivers.ps1
Unblock-File .\restore-drivers.ps1
```

Не рекомендуется использовать `Unrestricted` без необходимости.

Подробности: [`docs/execution-policy.md`](docs/execution-policy.md)

## Где сохраняются драйверы

По умолчанию резервная копия сохраняется на диске `C:`:

```text
C:\DriverBackups\<COMPUTERNAME>\<timestamp>\
```

Внутри создаются папки:

- `drivers` — экспортированные драйверы.
- `meta` — сведения о системе и контрольные данные.

## Восстановление

Скрипт `restore-drivers.ps1` использует встроенную утилиту Windows `pnputil` и устанавливает драйверы из указанной папки `drivers`, рекурсивно находя `.inf`-файлы.

Пример:

```powershell
.\restore-drivers.ps1 -DriversRoot "C:\DriverBackups\MYPC\2026-04-13_12-00\drivers"
```

Если допускается автоматическая перезагрузка при необходимости:

```powershell
.\restore-drivers.ps1 -DriversRoot "C:\DriverBackups\MYPC\2026-04-13_12-00\drivers" -AllowReboot
```

## Ограничения

- Экспортируются сторонние драйверы, а не полный образ системы.
- Это не заменяет полноценный системный backup.
- Драйверы GPU и chipset иногда лучше ставить свежими с сайта производителя.
- Старые драйверы могут не подойти после смены железа.

## Безопасность

- Скрипты должны запускаться от администратора.
- Перед запуском стоит прочитать содержимое `.ps1`-файлов.
- Не запускайте скрипты из непроверенных источников.

## License

MIT. См. файл [`LICENSE`](LICENSE).
