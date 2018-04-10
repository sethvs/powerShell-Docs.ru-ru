---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Использование конструктора ресурсов
ms.openlocfilehash: e0282671861755a5f147de4d07783a4680024ec5
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="using-the-resource-designer-tool"></a>Использование конструктора ресурсов

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Конструктор ресурсов — это набор командлетов, предоставляемых модулем **xDscResourceDesigner** и упрощающих создание ресурсов настройки требуемого состояния (DSC) Windows PowerShell. Командлеты в этом ресурсе помогают создать MOF-схему, модуль сценария и структуру папок для нового ресурса. Дополнительные сведения о ресурсах DSC см. в статье [Встроенные ресурсы настройки требуемого состояния (DSC) Windows PowerShell](authoringResource.md).
В этом разделе мы создадим ресурс DSC, управляющий пользователями Active Directory.
Для установки модуля **xDscResourceDesigner** используйте командлет [Install-Module](https://technet.microsoft.com/library/dn807162.aspx).

>**Примечание**. **Install-Module** включен в модуль **PowerShellGet**, содержащийся в PowerShell 5.0. Вы можете скачать модуль **PowerShellGet**для PowerShell 3.0 и 4.0 в разделе [Предварительная версия модулей PackageManagement PowerShell](https://www.microsoft.com/en-us/download/details.aspx?id=49186).

## <a name="creating-resource-properties"></a>Создание свойств ресурсов
В первую очередь необходимо решить, какие свойства будут представлены в ресурсе. В этом примере мы определим пользователя Active Directory со следующими свойствами.

Имя параметра Описание
* **UserName**: основное свойство, которое служит уникальным идентификатором пользователя.
* **Ensure**: указывает, должна ли учетная запись пользователя присутствовать (Present) или отсутствовать (Absent). Этот параметр имеет только два возможных значения.
* **DomainCredential**: доменный пароль для пользователя.
* **Password**: пароль для пользователя, позволяющий конфигурации при необходимости изменить пароль пользователя.

Для создания свойств используется командлет **New-xDscResourceProperty**. Описанные выше свойства создаются следующими командами PowerShell.

```powershell
$UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet “Present”, “Absent”
$DomainCredential = New-xDscResourceProperty –Name DomainCredential -Type PSCredential -Attribute Write
$Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## <a name="create-the-resource"></a>Создание ресурсов

Теперь, когда свойства ресурса созданы, можно вызвать командлет **New-xDscResource** для создания ресурса. Командлет **New-xDscResource** выводит список свойств в виде параметров. Кроме того, он принимает путь для создания модуля, имя нового ресурса и имя модуля, в котором он будет храниться. Ресурс создает следующая команда PowerShell.

```powershell
New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path ‘C:\Program Files\WindowsPowerShell\Modules’ –ModuleName Demo_DSCModule
```

Командлет **New-xDscResource** создает MOF-схему, каркас сценария для ресурса, необходимую структуру папок, а также манифест для модуля, предоставляющего новый ресурс.

MOF-схема находится в файле **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof** и имеет следующее содержание:

```
[ClassVersion("1.0.0.0"), FriendlyName("Demo_ADUser")]
class Demo_ADUser : OMI_BaseResource
{
  [Key] string UserName;
  [Write, ValueMap{"Present","Absent"}, Values{"Present","Absent"}] string Ensure;
  [Write, EmbeddedInstance("MSFT_Credential")] String DomainCredential;
  [Write, EmbeddedInstance("MSFT_Credential")] String Password;
};
```

Сценарий ресурса находится в файле **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**. Он не содержит фактической логики реализации ресурса — ее необходимо добавить самостоятельно. Каркас сценария выглядит следующим образом.

```powershell
function Get-TargetResource
{
  [CmdletBinding()]
  [OutputType([System.Collections.Hashtable])]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."


  <#
  $returnValue = @{
  UserName = [System.String]
  Ensure = [System.String]
  DomainAdminCredential = [System.Management.Automation.PSCredential]
  Password = [System.Management.Automation.PSCredential]
  }

  $returnValue
  #>
}


function Set-TargetResource
{
  [CmdletBinding()]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName,

    [ValidateSet("Present","Absent")]
    [System.String]
    $Ensure,

    [System.Management.Automation.PSCredential]
    $DomainAdminCredential,

    [System.Management.Automation.PSCredential]
    $Password
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."

  #Include this line if the resource requires a system reboot.
  #$global:DSCMachineStatus = 1


}


function Test-TargetResource
{
  [CmdletBinding()]
  [OutputType([System.Boolean])]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName,

    [ValidateSet("Present","Absent")]
    [System.String]
    $Ensure,

    [System.Management.Automation.PSCredential]
    $DomainAdminCredential,

    [System.Management.Automation.PSCredential]
    $Password
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."


  <#
  $result = [System.Boolean]

  $result
  #>
}


Export-ModuleMember -Function *-TargetResource
```

## <a name="updating-the-resource"></a>Обновление ресурса

Если вам нужно добавить или изменить список параметров для ресурса, используйте командлет **Update-xDscResource**. Этот командлет обновляет ресурс с учетом нового списка параметров. Если логика в сценарий ресурсов уже добавлена, она останется без изменений.

Предположим, вам нужно включить в ресурс время последнего входа пользователя. Вместо того чтобы писать ресурс заново, можно выполнить командлет **New-xDscResourceProperty**, чтобы создать еще одно свойство, а затем командлет **Update-xDscResource**, чтобы добавить его в список свойств.

```powershell
$lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description “For mapping users to their last log on time”
Update-xDscResource –Name ‘Demo_ADUser’ –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## <a name="testing-a-resource-schema"></a>Тестирование схемы ресурсов

Конструктор ресурсов предоставляет еще один командлет, который можно использовать для проверки работоспособности MOF-схемы, написанной вами вручную. Вызовите командлет **Test-xDscSchema**, передав в качестве параметра путь к MOF-схеме ресурса. Командлет выдаст все имеющиеся в схеме ошибки.

### <a name="see-also"></a>См. также

#### <a name="concepts"></a>Концепции
[Создание пользовательских ресурсов DSC Windows PowerShell](authoringResource.md)

#### <a name="other-resources"></a>Прочие ресурсы
[Модуль xDscResourceDesigner](https://powershellgallery.com/packages/xDscResourceDesigner)