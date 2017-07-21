---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
title: "Известные проблемы в WMF 5.1"
ms.openlocfilehash: 93113962781f1cc84a80f8f97f56ffd7622fec6b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="known-issues-in-wmf-51"></a><span data-ttu-id="c5b4e-103">Известные проблемы в WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="c5b4e-103">Known Issues in WMF 5.1</span></span> #

> <span data-ttu-id="c5b4e-104">Примечание. Эта информация может быть изменена.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-104">Note: This information is subject to change.</span></span>

## <a name="starting-powershell-shortcut-as-administrator"></a><span data-ttu-id="c5b4e-105">Запуск PowerShell от имени администратора с помощью ярлыка</span><span class="sxs-lookup"><span data-stu-id="c5b4e-105">Starting PowerShell shortcut as Administrator</span></span>
<span data-ttu-id="c5b4e-106">После установки WMF при попытке запустить PowerShell от имени администратора с помощью ярлыка может появиться сообщение "Неопознанная ошибка".</span><span class="sxs-lookup"><span data-stu-id="c5b4e-106">Upon installing WMF, if you try to start PowerShell as administrator from the shortcut, you may get an "Unspecified error" message.</span></span>
<span data-ttu-id="c5b4e-107">Повторно запустите PowerShell через ярлык без прав администратора. Теперь он работает и с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-107">Reopen the shortcut as non-administrator and the shortcut now works even as administrator.</span></span>

## <a name="pester"></a><span data-ttu-id="c5b4e-108">Pester</span><span class="sxs-lookup"><span data-stu-id="c5b4e-108">Pester</span></span>
<span data-ttu-id="c5b4e-109">В этом выпуске существует две проблемы, которые следует иметь в виду при использовании Pester на сервере Nano.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-109">In this release, there are two issues you should be aware of when using Pester on Nano Server:</span></span>

* <span data-ttu-id="c5b4e-110">Запуск тестов для самого Pester может привести к некоторым ошибкам из-за различий между FULL CLR и CORE CLR.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-110">Running tests against Pester itself can result in some failures because of differences between FULL CLR and CORE CLR.</span></span> <span data-ttu-id="c5b4e-111">В частности, для типа XmlDocument недоступен метод Validate.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-111">In particular, the Validate method is not available on the XmlDocument type.</span></span> <span data-ttu-id="c5b4e-112">Известно, что шесть проверок схемы журналов вывода NUnit завершаются сбоем.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-112">Six tests which attempt to validate the schema of the NUnit output logs are known to fail.</span></span> 
* <span data-ttu-id="c5b4e-113">Один из тестов объема протестированного кода сейчас завершается сбоем из-за того, что ресурс DSC *WindowsFeature* не существует на сервере Nano Server.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-113">One Code Coverage test fails currently because the *WindowsFeature* DSC Resource does not exist in Nano Server.</span></span> <span data-ttu-id="c5b4e-114">Тем не менее эти ошибки обычно носят информационный характер, и их можно спокойно пропустить.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-114">However, these failures are generally benign and can safely be ignored.</span></span>

## <a name="operation-validation"></a><span data-ttu-id="c5b4e-115">Проверка операций</span><span class="sxs-lookup"><span data-stu-id="c5b4e-115">Operation Validation</span></span> 

* <span data-ttu-id="c5b4e-116">Модуль Microsoft.PowerShell.Operation.Validation вызывает ошибку в командлете Update-Help, так как код URI справки не работает.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-116">Update-Help fails for Microsoft.PowerShell.Operation.Validation module due to non-working help URI</span></span>

## <a name="dsc-after-uninstall-wmf"></a><span data-ttu-id="c5b4e-117">DSC после удаления WMF</span><span class="sxs-lookup"><span data-stu-id="c5b4e-117">DSC after uninstall WMF</span></span> 
* <span data-ttu-id="c5b4e-118">Удаление WMF не удаляет MOF-документы DSC из папки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-118">Uninstalling WMF does not delete DSC MOF documents from the configuration folder.</span></span> <span data-ttu-id="c5b4e-119">DSC не будет правильно работать, если MOF-документы содержат более новые свойства, которые недоступны в старых системах.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-119">DSC won't work properly if the MOF documents contain newer properties which are not available on the older systems.</span></span> <span data-ttu-id="c5b4e-120">В этом случае запустите скрипт из консоли PowerShell с повышенными правами, чтобы очистить состояния DSC.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-120">In this case, run the following script from elevated PowerShell console to to clean up the DSC states.</span></span>
 ```PowerShell
    $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
            "$env:windir\system32\configuration\*.mof.checksum",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
           )

    $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
 ```  

## <a name="jea-virtual-accounts"></a><span data-ttu-id="c5b4e-121">Виртуальные учетные записи JEA</span><span class="sxs-lookup"><span data-stu-id="c5b4e-121">JEA Virtual Accounts</span></span>
<span data-ttu-id="c5b4e-122">В конечных точках и конфигурациях сеанса JEA, в которых настроено использование виртуальных учетных записей в WMF 5.0, не будет настроено использование виртуальной учетной записи после обновления до WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-122">JEA endpoints and session configurations configured to use virtual accounts in WMF 5.0 will not be configured to use a virtual account after upgrading to WMF 5.1.</span></span>
<span data-ttu-id="c5b4e-123">Это означает, что команды, запускаемые в сеансах JEA, будут запускаться в удостоверении подключающегося пользователя, а не в учетной записи временного администратора. Это может препятствовать запуску команд, требующих повышенных прав.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-123">This means that commands run in JEA sessions will run under the connecting user's identity instead of a temporary administrator account, potentially preventing the user from running commands which require elevated privileges.</span></span>
<span data-ttu-id="c5b4e-124">Чтобы восстановить виртуальные учетные записи, нужно отменить регистрацию и повторно зарегистрировать все конфигурации сеанса, использующие виртуальные учетные записи.</span><span class="sxs-lookup"><span data-stu-id="c5b4e-124">To restore the virtual accounts, you need to unregister and re-register any session configurations that use virtual accounts.</span></span>

```powershell
# Find the JEA endpoint by its name
$jea = Get-PSSessionConfiguration -Name MyJeaEndpoint

# Copy the cached PSSC file so it can be re-registered
$pssc = Copy-Item $jea.ConfigFilePath $env:temp -PassThru

# Unregister the current PSSC
Unregister-PSSessionConfiguration -Name $jea.Name

# Re-register the PSSC
Register-PSSessionConfiguration -Name $jea.Name -Path $pssc.FullName -Force

# Ensure the access policies remain the same
Set-PSSessionConfiguration -Name $newjea.Name -SecurityDescriptorSddl $jea.SecurityDescriptorSddl
```

