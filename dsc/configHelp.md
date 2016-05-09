# Запись поддержки конфигураций DSC

>Область применения: Windows PowerShell 5.0

Вы можете использовать справку на основе комментариев в конфигурациях DSC. Пользователи могут получить доступ к справке, вызвав функцию конфигурации с `-?` или с помощью 
Командлет [Get-Help](https://technet.microsoft.com/en-us/library/hh849696.aspx). Дополнительные сведения о справке на основе комментариев PowerShell см. в 
[about_Comment_Based_Help](https://technet.microsoft.com/en-us/library/hh847834.aspx).

В следующем примере показан сценарий, который содержит две конфигурации и справку на основе комментариев для каждой конфигурации:

```powershell
<#
.SYNOPSIS
A brief description of the function or script. This keyword can be used only once for each configuration.


.DESCRIPTION
A detailed description of the function or script. This keyword can be used only once for each configuration.


.PARAMETER computername
The description of a parameter. Add a .PARAMETER keyword for each parameter in the function or script syntax.

Type the parameter name on the same line as the .PARAMETER keyword. Type the parameter description on the lines following the .PARAMETER keyword. 
Windows PowerShell interprets all text between the .PARAMETER line and the next keyword or the end of the comment block as part of the parameter description. 
The description can include paragraph breaks.

The Parameter keywords can appear in any order in the comment block, but the function or script syntax determines the order in which the parameters 
(and their descriptions) appear in help topic. To change the order, change the syntax.

.PARAMETER filePath
Provide a PARAMETER section for each parameter that your script or function accepts.

.EXAMPLE
A sample command that uses the function or script, optionally followed by sample output and a description. Repeat this keyword for each example. If you have multiple examples,
there is no need to number them. PowerShell will number the examples in help text.

.EXAMPLE
This example will be labeled "EXAMPLE 2" when help is displayed to the user.
#>

configuration HelpSample1
{
    param([string]$computername,[string]$filePath)
    File f
    {
        Contents="Hello World"
        DestinationPath = "c:\Destination.txt"
    }
}
```

## Просмотр справки по конфигурации

Для просмотра справки по конфигурации используйте командлет **Get-Help** с именем функции или введите имя функции и `-?`. Ниже приведены выходные данные
предыдущей функции при передаче в **Get-Help**:

```powershell
PS C:\> Get-Help HelpSample1

NAME
    HelpSample1
    
SYNOPSIS
    A brief description of the function or script. This keyword can be used only once for each configuration.
    
    
SYNTAX
    HelpSample1 [[-InstanceName] <String>] [[-DependsOn] <String[]>] [[-OutputPath] <String>] [[-ConfigurationData] <Hashtable>] [[-computername] 
    <String>] [[-filePath] <String>] [<CommonParameters>]
    
    
DESCRIPTION
    A detailed description of the function or script. This keyword can be used only once for each configuration.
    

RELATED LINKS

REMARKS
    To see the examples, type: "get-help HelpSample1 -examples".
    For more information, type: "get-help HelpSample1 -detailed".
    For technical information, type: "get-help HelpSample1 -full".
```

## См. также
* [Конфигурации DSC](configurations.md)

<!--HONumber=Apr16_HO5-->


