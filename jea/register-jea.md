---
ms.date: 2017-06-12
author: rpsqrd
ms.topic: conceptual
keywords: "jea,powershell,безопасность"
title: "Регистрация конфигураций JEA"
ms.openlocfilehash: 0684a1c7acffbccbedab9dba4689611a24c8ae25
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="registering-jea-configurations"></a>Регистрация конфигураций JEA

> Область применения: Windows PowerShell 5.0

Последний шаг перед использованием JEA после создания [возможностей роли](role-capabilities.md) и [файла конфигурации сеанса](session-configurations.md) заключается в регистрации конечной точки JEA.
Этот процесс применяет параметры конфигурации сеанса в системе и делает конечную точку доступной пользователям и модулям автоматизации.

## <a name="single-machine-configuration"></a>Конфигурация для отдельного компьютера

Для небольших сред можно развернуть JEA, зарегистрировав файл конфигурации сеанса с помощью командлета [Register-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration).

Прежде чем приступать к этой процедуре, убедитесь, что выполняются следующие необходимые условия:
- Создана одна или несколько ролей, которые помещены в папку "RoleCapabilities" для допустимого модуля PowerShell.
- Создан и проверен файл конфигурации сеанса.
- Пользователь, регистрирующий конфигурацию JEA, обладает правами администратора в соответствующих системах.

Кроме того, потребуется выбрать имя для конечной точки JEA.
Это имя будет запрашиваться при подключении пользователей к системе с помощью JEA.
Для просмотра имен существующих конечных точек в системе можно использовать командлет [Get-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration).
Конечные точки, начинающиеся со слова "microsoft", обычно поставляются с Windows.
Конечная точка "microsoft.powershell" используется по умолчанию при подключении к удаленной конечной точке PowerShell.

```powershell
PS C:\> Get-PSSessionConfiguration | Select-Object Name

Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

После определения имени для конечной точки JEA выполните приведенную ниже команду, чтобы зарегистрировать конечную точку.

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> Приведенная выше команда перезапускает службу WinRM в системе.
> При этом завершаются все сеансы удаленного взаимодействия PowerShell, а также любые текущие конфигурации DSC.
> Перед выполнением этой команды рекомендуется перевести рабочие компьютеры в автономный режим, чтобы избежать нарушения бизнес-операции.

Если регистрация прошла успешно, можно приступать к [использованию JEA](using-jea.md).
Файл конфигурации сеанса можно удалить в любое время, так как после регистрации он не используется.

## <a name="multi-machine-configuration-with-dsc"></a>Конфигурация для нескольких компьютеров с помощью DSC

Если JEA развертывается на нескольких компьютерах, самая простая модель развертывания заключается в использовании ресурса [настройки требуемого состояния](https://msdn.microsoft.com/en-us/powershell/dsc/overview) JEA, позволяющего быстро и согласованно развернуть JEA на каждом компьютере.

Чтобы развернуть JEA с помощью DSC, следует убедиться в выполнении следующих условий:
- Создана одна или несколько возможностей ролей, которые были добавлены в допустимый модуль PowerShell.
- Модуль PowerShell, содержащий нужные роли, хранится в (доступной только для чтения) общей папке, видимой каждому компьютеру.
- Были определены параметры для конфигурации сеанса. При использовании ресурса DSC JEA создавать файл конфигурации сеанса не требуется.
- Вы имеете учетные данные, которые позволяют выполнять административные действия на каждом компьютере, или доступ к опрашивающему серверу DSC, используемому для управления компьютерами.
- Вы загрузили [ресурс DSC JEA](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource).

На целевом компьютере (или опрашивающем сервере, если вы используете его) создайте конфигурацию DSC для конечной точки JEA.
В этой конфигурации используйте ресурс DSC JustEnoughAdministration для настройки файла конфигурации сеанса и ресурс File для копирования возможностей ролей из общей папки.

С помощью ресурса DSC можно настраивать следующие свойства:
- Определения ролей
- Группы виртуальных учетных записей
- Имя групповой управляемой учетной записи службы
- Каталог записей
- Диск пользователя
- Правила условного доступа
- Сценарии запуска для сеанса JEA

Синтаксис для каждого из этих свойств в конфигурации DSC согласуется с файлом конфигурации сеанса PowerShell.

Ниже приведен пример конфигурации DSC для модуля общего обслуживания сервера.

Предполагается, что допустимый модуль PowerShell, содержащий возможности ролей во вложенной папке "RoleCapabilities", находится в общей папке "\\\\myfileshare\\JEA".


```powershell
Configuration JEAMaintenance
{
    Import-DscResource -Module JustEnoughAdministration, PSDesiredStateConfiguration

    File MaintenanceModule
    {
        SourcePath = "\\myfileshare\JEA\ContosoMaintenance"
        DestinationPath = "C:\Program Files\WindowsPowerShell\Modules\ContosoMaintenance"
        Checksum = "SHA-256"
        Ensure = "Present"
        Type = "Directory"
        Recurse = $true
    }

    JeaEndpoint JEAMaintenanceEndpoint
    {
        EndpointName = "JEAMaintenance"
        RoleDefinitions = "@{ 'CONTOSO\JEAMaintenanceAuditors' = @{ RoleCapabilities = 'GeneralServerMaintenance-Audit' }; 'CONTOSO\JEAMaintenanceAdmins' = @{ RoleCapabilities = 'GeneralServerMaintenance-Audit', 'GeneralServerMaintenance-Admin' } }"
        TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
        DependsOn = '[File]MaintenanceModule'
    }
}
```

Затем эту конфигурацию можно применить в системе, [напрямую вызвав локальный диспетчер конфигураций](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) или обновив [конфигурацию опрашивающего сервера](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver).

Ресурс DSC также позволяет заменить конечную точку удаленного взаимодействия по умолчанию Microsoft.PowerShell.
В этом случае ресурс автоматически регистрирует резервную конечную точку без ограничений с именем "Microsoft.PowerShell.Restricted", имеющую ACL WinRM по умолчанию (который предоставляет членам групп "Локальные администраторы" и "Пользователи удаленного управления" доступ к ней).

## <a name="unregistering-jea-configurations"></a>Отмена регистрации конфигураций JEA

Чтобы удалить конечную точку JEA из системы, используйте командлет [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration).
Отмена регистрации конечной точки JEA не позволит новым пользователям создавать новые сеансы JEA в системе.
Кроме того, вы можете обновить конфигурацию JEA, повторно зарегистрировав измененный файл конфигурации сеанса с использованием такого же имени конечной точки.

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> Отмена регистрации конечной точки JEA вызывает перезапуск службы WinRM.
> Это приведет к прерыванию большинства выполняемых операций удаленного управления, включая другие сеансы PowerShell, вызовы WMI и некоторые средства управления.
> Отменяйте регистрацию конечных точек PowerShell только во время запланированных периодов обслуживания.

## <a name="next-steps"></a>Дальнейшие действия

- [Тестирование конечной точки JEA](using-jea.md)

