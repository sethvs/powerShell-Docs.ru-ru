# Поддержка автоматического запуска от имени для ресурсов DSC
Поддержка учетных данных запуска от имени DSC
--------------------------------

Версия WMF 5.0 Preview за апрель 2015 г. включает в себя поддержку выполнения **любого** ресурса DSC с заданным набором учетных данных с помощью свойства PsDscRunAsCredential. Это делает доступными такие сценарии, как установка пакетов MSI в контексте определенного пользователя, доступ к кусту реестра пользователя, доступ к определенному локальному каталогу пользователя, доступ к сетевой папке и т. д.

Ниже приведен пример использования свойства PsDscRunAsCredential в DSC для изменения цвета фона пользователя командной строки у пользователя.

Configuration ChangeCmdBackGroundColor

{

    Node ("localhost")

    {

        Registry CmdPath

        {

            Key = "HKEY\_CURRENT\_USER\\\\Software\\Microsoft\\\\Command Processor"

            ValueName = "DefaultColor"

            ValueData = '1F'

            ValueType = "DWORD"

            Ensure = "Present"

            Force = $true

            Hex = $true

            PsDscRunAsCredential = get-credential

        }

    }

}

$configData = @{

AllNodes = @(

@{

NodeName="localhost";

CertificateFile = "C:\\publicKeys\\targetNode.cer"

}

)

}

ChangeCmdBackGroundColor -ConfigurationData $configData

## Известные проблемы

Ниже перечислены известные с проблемы учетными данными запуска от имени DSC в этом выпуске:

-   Ресурс WindowsProcess не поддерживает учетные данные запуска от имени.

<!--HONumber=Mar16_HO2-->
