---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Запуск DSC с учетными данными пользователя
ms.openlocfilehash: 37e6ff64c9c6d3960653d417e22a6c93c653230c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="running-dsc-with-user-credentials"></a><span data-ttu-id="09e2f-103">Запуск DSC с учетными данными пользователя</span><span class="sxs-lookup"><span data-stu-id="09e2f-103">Running DSC with user credentials</span></span>

> <span data-ttu-id="09e2f-104">Область применения: Windows PowerShell 5.0, Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="09e2f-104">Applies To: Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="09e2f-105">Ресурс DSC можно запускать с определенным набором учетных данных. Для этого используется автоматическое свойство **PsDscRunAsCredential** в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="09e2f-105">You can run a DSC resource under a specified set of credentials by using the automatic **PsDscRunAsCredential** property in the configuration.</span></span>
<span data-ttu-id="09e2f-106">По умолчанию DSC запускает каждый ресурс в качестве системной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="09e2f-106">By default, DSC runs each resource as the system account.</span></span>
<span data-ttu-id="09e2f-107">Иногда бывает необходим запуск с учетной записью обычного пользователя, например, при установке MSI-пакетов в контексте определенного пользователя, при установке разделов реестра пользователя, доступе к конкретному локальному каталогу пользователя или сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="09e2f-107">There are times when running as a user is necessary, such as installing MSI packages in a specific user context, setting a user's registry keys, accessing a user's specific local directory, or accessing a network share.</span></span>

<span data-ttu-id="09e2f-108">У каждого ресурса есть свойство **PsDscRunAsCredential**, которому можно назначить учетные данные любого пользователя (объект [PSCredential](https://msdn.microsoft.com/library/ms572524(v=VS.85).aspx)).</span><span class="sxs-lookup"><span data-stu-id="09e2f-108">Every DSC resource has a **PsDscRunAsCredential** property that can be set to any user credentials (a [PSCredential](https://msdn.microsoft.com/library/ms572524(v=VS.85).aspx) object).</span></span>
<span data-ttu-id="09e2f-109">Учетные данные можно жестко задать в качестве значения свойства конфигурации или установить в качестве значения [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx). В этом случае пользователю будет предложено ввести учетные данные при компиляции конфигурации (дополнительные сведения о компиляции конфигураций см. в разделе [Конфигурации](configurations.md)).</span><span class="sxs-lookup"><span data-stu-id="09e2f-109">The credential can be hard-coded as the value of the property in the configuration, or you can set the value to [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx), which will prompt the user for a credential when the configuration is compiled (for information about compiling configurations, see [Configurations](configurations.md).</span></span>

><span data-ttu-id="09e2f-110">**Примечание**. В PowerShell 5.0 использование свойства **PsDscRunAsCredential** в конфигурациях, вызывающих составные ресурсы, не поддерживалось.</span><span class="sxs-lookup"><span data-stu-id="09e2f-110">**Note:** In PowerShell 5.0, using the **PsDscRunAsCredential** property in configurations calling composite resources was not supported.</span></span>
><span data-ttu-id="09e2f-111">В PowerShell 5.1 свойство **PsDscRunAsCredential** поддерживается в конфигурациях, вызывающих составные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="09e2f-111">In PowerShell 5.1, the **PsDscRunAsCredential** property is supported in configurations calling composite resources.</span></span>

><span data-ttu-id="09e2f-112">**Примечание**. Свойство **PsDscRunAsCredential** недоступно в PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="09e2f-112">**Note:** The **PsDscRunAsCredential** property is not available in PowerShell 4.0.</span></span>

<span data-ttu-id="09e2f-113">В следующем примере **Get-Credential** используется для запроса учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="09e2f-113">In the following example, **Get-Credential** is used to prompt the user for credentials.</span></span>
<span data-ttu-id="09e2f-114">Ресурс [Registry](registryResource.md) используется для изменения раздела реестра, указывающего цвет фона для окна командной строки Windows.</span><span class="sxs-lookup"><span data-stu-id="09e2f-114">The [Registry](registryResource.md) resource is used to change the registry key that specifies the background color for the Windows command prompt window.</span></span>

```powershell
Configuration ChangeCmdBackGroundColor
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        Registry CmdPath
        {
            Key                  = 'HKEY_CURRENT_USER\SOFTWARE\Microsoft\Command Processor'
            ValueName            = 'DefaultColor'
            ValueData            = '1F'
            ValueType            = 'DWORD'
            Ensure               = 'Present'
            Force                = $true
            Hex                  = $true
            PsDscRunAsCredential = Get-Credential
        }
    }
}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost';
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}

ChangeCmdBackGroundColor -ConfigurationData $configData
```
><span data-ttu-id="09e2f-115">**Примечание**. В этом примере предполагается, что у вас есть действительный сертификат в `C:\publicKeys\targetNode.cer` и что отображаемое значение представляет собой отпечаток этого сертификата.</span><span class="sxs-lookup"><span data-stu-id="09e2f-115">**Note:** This example assumes that you have a valid certificate at `C:\publicKeys\targetNode.cer`, and that the thumbprint of that certificate is the value shown.</span></span>
><span data-ttu-id="09e2f-116">Сведения о шифровании учетных данных в MOF-файлах конфигурации DSC см. в разделе [Защита MOF-файла](secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="09e2f-116">For information about encrypting credentials in DSC configuration MOF files, see [Securing the MOF file](secureMOF.md).</span></span>