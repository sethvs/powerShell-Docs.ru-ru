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
# <a name="registering-jea-configurations"></a><span data-ttu-id="b7ee8-103">Регистрация конфигураций JEA</span><span class="sxs-lookup"><span data-stu-id="b7ee8-103">Registering JEA Configurations</span></span>

> <span data-ttu-id="b7ee8-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b7ee8-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="b7ee8-105">Последний шаг перед использованием JEA после создания [возможностей роли](role-capabilities.md) и [файла конфигурации сеанса](session-configurations.md) заключается в регистрации конечной точки JEA.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-105">The last step before you can use JEA once you have your [role capabilities](role-capabilities.md) and [session configuration file](session-configurations.md) created is to register the JEA endpoint.</span></span>
<span data-ttu-id="b7ee8-106">Этот процесс применяет параметры конфигурации сеанса в системе и делает конечную точку доступной пользователям и модулям автоматизации.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-106">This process applies the session configuration information to the system and makes the endpoint available for use by users and automation engines.</span></span>

## <a name="single-machine-configuration"></a><span data-ttu-id="b7ee8-107">Конфигурация для отдельного компьютера</span><span class="sxs-lookup"><span data-stu-id="b7ee8-107">Single machine configuration</span></span>

<span data-ttu-id="b7ee8-108">Для небольших сред можно развернуть JEA, зарегистрировав файл конфигурации сеанса с помощью командлета [Register-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration).</span><span class="sxs-lookup"><span data-stu-id="b7ee8-108">For small environments, you can deploy JEA by registering the session configuration file using the [Register-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) cmdlet.</span></span>

<span data-ttu-id="b7ee8-109">Прежде чем приступать к этой процедуре, убедитесь, что выполняются следующие необходимые условия:</span><span class="sxs-lookup"><span data-stu-id="b7ee8-109">Before you begin, ensure that the following prerequisites have been met:</span></span>
- <span data-ttu-id="b7ee8-110">Создана одна или несколько ролей, которые помещены в папку "RoleCapabilities" для допустимого модуля PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-110">One or more roles has been created and placed in the 'RoleCapabilities' folder of a valid PowerShell module.</span></span>
- <span data-ttu-id="b7ee8-111">Создан и проверен файл конфигурации сеанса.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-111">A session configuration file has been created and tested.</span></span>
- <span data-ttu-id="b7ee8-112">Пользователь, регистрирующий конфигурацию JEA, обладает правами администратора в соответствующих системах.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-112">The user registering the JEA configuration has administrator rights on the system(s).</span></span>

<span data-ttu-id="b7ee8-113">Кроме того, потребуется выбрать имя для конечной точки JEA.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-113">You will also need to select a name for your JEA endpoint.</span></span>
<span data-ttu-id="b7ee8-114">Это имя будет запрашиваться при подключении пользователей к системе с помощью JEA.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-114">The name of the JEA endpoint will be required when users want to connect to the system using JEA.</span></span>
<span data-ttu-id="b7ee8-115">Для просмотра имен существующих конечных точек в системе можно использовать командлет [Get-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration).</span><span class="sxs-lookup"><span data-stu-id="b7ee8-115">You can use the [Get-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) cmdlet to check the names of existing endpoints on the system.</span></span>
<span data-ttu-id="b7ee8-116">Конечные точки, начинающиеся со слова "microsoft", обычно поставляются с Windows.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-116">Endpoints that start with 'microsoft' are typically shipped with Windows.</span></span>
<span data-ttu-id="b7ee8-117">Конечная точка "microsoft.powershell" используется по умолчанию при подключении к удаленной конечной точке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-117">The 'microsoft.powershell' endpoint is the default endpoint used when connecting to a remote PowerShell endpoint.</span></span>

```powershell
PS C:\> Get-PSSessionConfiguration | Select-Object Name

Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

<span data-ttu-id="b7ee8-118">После определения имени для конечной точки JEA выполните приведенную ниже команду, чтобы зарегистрировать конечную точку.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-118">When you have determined an appropriate name for your JEA endpoint, run the following command to register the endpoint.</span></span>

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="b7ee8-119">Приведенная выше команда перезапускает службу WinRM в системе.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-119">The above command will restart the WinRM service on the system.</span></span>
> <span data-ttu-id="b7ee8-120">При этом завершаются все сеансы удаленного взаимодействия PowerShell, а также любые текущие конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-120">This will terminate all PowerShell remoting sessions as well as any ongoing DSC configurations.</span></span>
> <span data-ttu-id="b7ee8-121">Перед выполнением этой команды рекомендуется перевести рабочие компьютеры в автономный режим, чтобы избежать нарушения бизнес-операции.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-121">It is recommended that you take any production machines offline before running the command to avoid disrupting business operations.</span></span>

<span data-ttu-id="b7ee8-122">Если регистрация прошла успешно, можно приступать к [использованию JEA](using-jea.md).</span><span class="sxs-lookup"><span data-stu-id="b7ee8-122">If registration was successful, you are ready to [use JEA](using-jea.md).</span></span>
<span data-ttu-id="b7ee8-123">Файл конфигурации сеанса можно удалить в любое время, так как после регистрации он не используется.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-123">You may delete the session configuration file at any time; it is not used after registration.</span></span>

## <a name="multi-machine-configuration-with-dsc"></a><span data-ttu-id="b7ee8-124">Конфигурация для нескольких компьютеров с помощью DSC</span><span class="sxs-lookup"><span data-stu-id="b7ee8-124">Multi-machine configuration with DSC</span></span>

<span data-ttu-id="b7ee8-125">Если JEA развертывается на нескольких компьютерах, самая простая модель развертывания заключается в использовании ресурса [настройки требуемого состояния](https://msdn.microsoft.com/en-us/powershell/dsc/overview) JEA, позволяющего быстро и согласованно развернуть JEA на каждом компьютере.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-125">If you are deploying JEA on multiple machines, the simplest deployment model is to use the JEA [Desired State Configuration](https://msdn.microsoft.com/en-us/powershell/dsc/overview) resource to quickly and consistently deploy JEA on each machine.</span></span>

<span data-ttu-id="b7ee8-126">Чтобы развернуть JEA с помощью DSC, следует убедиться в выполнении следующих условий:</span><span class="sxs-lookup"><span data-stu-id="b7ee8-126">To deploy JEA with DSC, you will need to ensure the following prerequisites are met:</span></span>
- <span data-ttu-id="b7ee8-127">Создана одна или несколько возможностей ролей, которые были добавлены в допустимый модуль PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-127">One or more role capabilities have been authored and added to a valid PowerShell module.</span></span>
- <span data-ttu-id="b7ee8-128">Модуль PowerShell, содержащий нужные роли, хранится в (доступной только для чтения) общей папке, видимой каждому компьютеру.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-128">The PowerShell module containing the roles is stored on a (read-only) file share accessible by each machine.</span></span>
- <span data-ttu-id="b7ee8-129">Были определены параметры для конфигурации сеанса.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-129">Settings for the session configuration have been determined.</span></span> <span data-ttu-id="b7ee8-130">При использовании ресурса DSC JEA создавать файл конфигурации сеанса не требуется.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-130">You do not need to create a session configuration file when using the JEA DSC resource.</span></span>
- <span data-ttu-id="b7ee8-131">Вы имеете учетные данные, которые позволяют выполнять административные действия на каждом компьютере, или доступ к опрашивающему серверу DSC, используемому для управления компьютерами.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-131">You have credentials that will allow you to perform administrative actions on each machine, or have access to a DSC pull server used to manage the machines.</span></span>
- <span data-ttu-id="b7ee8-132">Вы загрузили [ресурс DSC JEA](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource).</span><span class="sxs-lookup"><span data-stu-id="b7ee8-132">You have downloaded the [JEA DSC resource](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)</span></span>

<span data-ttu-id="b7ee8-133">На целевом компьютере (или опрашивающем сервере, если вы используете его) создайте конфигурацию DSC для конечной точки JEA.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-133">On a target machine (or pull server, if you are using one), create a DSC configuration for your JEA endpoint.</span></span>
<span data-ttu-id="b7ee8-134">В этой конфигурации используйте ресурс DSC JustEnoughAdministration для настройки файла конфигурации сеанса и ресурс File для копирования возможностей ролей из общей папки.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-134">In this configuration, you will use the JustEnoughAdministration DSC resource to set up the session configuration file and the File resource to copy over the role capabilities from the file share.</span></span>

<span data-ttu-id="b7ee8-135">С помощью ресурса DSC можно настраивать следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="b7ee8-135">The following properties are configurable using the DSC resource:</span></span>
- <span data-ttu-id="b7ee8-136">Определения ролей</span><span class="sxs-lookup"><span data-stu-id="b7ee8-136">Role Definitions</span></span>
- <span data-ttu-id="b7ee8-137">Группы виртуальных учетных записей</span><span class="sxs-lookup"><span data-stu-id="b7ee8-137">Virtual Account groups</span></span>
- <span data-ttu-id="b7ee8-138">Имя групповой управляемой учетной записи службы</span><span class="sxs-lookup"><span data-stu-id="b7ee8-138">Group Managed Service Account name</span></span>
- <span data-ttu-id="b7ee8-139">Каталог записей</span><span class="sxs-lookup"><span data-stu-id="b7ee8-139">Transcript directory</span></span>
- <span data-ttu-id="b7ee8-140">Диск пользователя</span><span class="sxs-lookup"><span data-stu-id="b7ee8-140">User drive</span></span>
- <span data-ttu-id="b7ee8-141">Правила условного доступа</span><span class="sxs-lookup"><span data-stu-id="b7ee8-141">Conditional access rules</span></span>
- <span data-ttu-id="b7ee8-142">Сценарии запуска для сеанса JEA</span><span class="sxs-lookup"><span data-stu-id="b7ee8-142">Startup scripts for the JEA session</span></span>

<span data-ttu-id="b7ee8-143">Синтаксис для каждого из этих свойств в конфигурации DSC согласуется с файлом конфигурации сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-143">The syntax for each of these properties in a DSC configuration is consistent with the PowerShell session configuration file.</span></span>

<span data-ttu-id="b7ee8-144">Ниже приведен пример конфигурации DSC для модуля общего обслуживания сервера.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-144">Below is a sample DSC configuration for a general server maintenance module.</span></span>

<span data-ttu-id="b7ee8-145">Предполагается, что допустимый модуль PowerShell, содержащий возможности ролей во вложенной папке "RoleCapabilities", находится в общей папке "\\\\myfileshare\\JEA".</span><span class="sxs-lookup"><span data-stu-id="b7ee8-145">It assumes that a valid PowerShell module containing role capabilities in a 'RoleCapabilities' subfolder is located on the '\\\\myfileshare\\JEA' file share.</span></span>


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

<span data-ttu-id="b7ee8-146">Затем эту конфигурацию можно применить в системе, [напрямую вызвав локальный диспетчер конфигураций](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) или обновив [конфигурацию опрашивающего сервера](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver).</span><span class="sxs-lookup"><span data-stu-id="b7ee8-146">This configuration can then be applied on a system by [directly invoking the Local Configuration Manager](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) or updating the [pull server configuration](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver).</span></span>

<span data-ttu-id="b7ee8-147">Ресурс DSC также позволяет заменить конечную точку удаленного взаимодействия по умолчанию Microsoft.PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-147">The DSC resource also allows you to replace the default Microsoft.PowerShell remoting endpoint.</span></span>
<span data-ttu-id="b7ee8-148">В этом случае ресурс автоматически регистрирует резервную конечную точку без ограничений с именем "Microsoft.PowerShell.Restricted", имеющую ACL WinRM по умолчанию (который предоставляет членам групп "Локальные администраторы" и "Пользователи удаленного управления" доступ к ней).</span><span class="sxs-lookup"><span data-stu-id="b7ee8-148">If you do this, the resource will automatically register a backup unconstrainted endpoint named "Microsoft.PowerShell.Restricted" which has the default WinRM ACL (allowing Remote Management Users and local Administrators group members to access it).</span></span>

## <a name="unregistering-jea-configurations"></a><span data-ttu-id="b7ee8-149">Отмена регистрации конфигураций JEA</span><span class="sxs-lookup"><span data-stu-id="b7ee8-149">Unregistering JEA configurations</span></span>

<span data-ttu-id="b7ee8-150">Чтобы удалить конечную точку JEA из системы, используйте командлет [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration).</span><span class="sxs-lookup"><span data-stu-id="b7ee8-150">To remove a JEA endpoint on a system, use the [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) cmdlet.</span></span>
<span data-ttu-id="b7ee8-151">Отмена регистрации конечной точки JEA не позволит новым пользователям создавать новые сеансы JEA в системе.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-151">Unregistering a JEA endpoint will prevent new users from creating new JEA sessions on the system.</span></span>
<span data-ttu-id="b7ee8-152">Кроме того, вы можете обновить конфигурацию JEA, повторно зарегистрировав измененный файл конфигурации сеанса с использованием такого же имени конечной точки.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-152">It also allows you to update a JEA configuration by re-registering an updated session configuration file using the same endpoint name.</span></span>

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="b7ee8-153">Отмена регистрации конечной точки JEA вызывает перезапуск службы WinRM.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-153">Unregistering a JEA endpoint will cause the WinRM service to restart.</span></span>
> <span data-ttu-id="b7ee8-154">Это приведет к прерыванию большинства выполняемых операций удаленного управления, включая другие сеансы PowerShell, вызовы WMI и некоторые средства управления.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-154">This will interrupt most remote management operations in progress, including other PowerShell sessions, WMI invocations, and some management tools.</span></span>
> <span data-ttu-id="b7ee8-155">Отменяйте регистрацию конечных точек PowerShell только во время запланированных периодов обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b7ee8-155">Only unregister PowerShell endpoints during planned maintenance windows.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7ee8-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b7ee8-156">Next steps</span></span>

- [<span data-ttu-id="b7ee8-157">Тестирование конечной точки JEA</span><span class="sxs-lookup"><span data-stu-id="b7ee8-157">Test the JEA endpoint</span></span>](using-jea.md)

