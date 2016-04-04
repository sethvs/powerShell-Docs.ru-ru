# Запуск DSC с учетными данными пользователя 

> Область применения: Windows PowerShell 5.0

Конфигурацию DSC можно запустить с заданным набором учетных данных. Для этого используется свойство PsDscRunAsCredential в конфигурации. По умолчанию DSC запускается
с системной учетной записью. Иногда необходимо запустить ее с учетной записью обычного пользователя, например: при установке MSI-пакетов в контексте определенного пользователя, при установке разделов реестра пользователя,
при доступе к локальному каталогу определенного пользователя или при доступе к сетевой папке.

У каждого ресурса есть свойство PsDscRunAsCredential, которому можно присвоить учетные данные любого пользователя (объект PSCredential).
Учетные данные можно жестко закодировать в значении свойства конфигурации или установить в качестве значения Get-Credential,
в этом случае пользователю будет предложено ввести учетные данные при компиляции конфигурации (дополнительные сведения о компиляции конфигурации в разделе Конфигурации).

>Примечание. Свойство PsDscRunAsCredential недоступно в PowerShell 4.0.

В следующем примере Get-Credential используется для запроса учетных данных пользователя. Ресурс Registry используется для изменения раздела реестра, указывающего цвет фона
для окна командной строки Windows.

```powershell
Configuration ChangeCmdBackGroundColor    

{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName

    {
        Registry CmdPath

        {

            Key = 'HKEY_CURRENT_USER\SOFTWARE\Microsoft\Command Processor'

            ValueName = "DefaultColor"

            ValueData = '1F'

            ValueType = "DWORD"

            Ensure = "Present"

            Force = $true

            Hex = $true

            PsDscRunAsCredential = Get-Credential
        }
    }                   
}

$configData = @{

    AllNodes = @(

    @{

        NodeName="localhost";
        PSDscAllowDomainUser = $true
        CertificateFile = "C:\publicKeys\targetNode.cer"
        Thumbprint = "7ee7f09d-4be0-41aa-a47f-96b9e3bdec25"

    })

}

ChangeCmdBackGroundColor -ConfigurationData $configData
```
>Примечание. В этом примере предполагается, что у вас есть действительный сертификат в `C:\publicKeys\targetNode.cer` и что отображаемое значение представляет собой отпечаток этого сертификата.
>Сведения о шифровании учетных данных в MOF-файлах конфигурации DSC см. в разделе Защита MOF-файла. 



<!--HONumber=Mar16_HO2-->


