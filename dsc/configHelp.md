---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Запись поддержки конфигураций DSC"
ms.openlocfilehash: bcf5c4b1af3cfd8d2e6376c1b7344c7babcaba9a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="writing-help-for-dsc-configurations"></a><span data-ttu-id="fb494-103">Запись поддержки конфигураций DSC</span><span class="sxs-lookup"><span data-stu-id="fb494-103">Writing help for DSC configurations</span></span>

><span data-ttu-id="fb494-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="fb494-104">Applies To: Windows Windows PowerShell 5.0</span></span>

<span data-ttu-id="fb494-105">Вы можете использовать справку на основе комментариев в конфигурациях DSC.</span><span class="sxs-lookup"><span data-stu-id="fb494-105">You can use comment-based help in DSC configurations.</span></span> <span data-ttu-id="fb494-106">Пользователи могут получить доступ к справке, вызвав функцию конфигурации с `-?` или с помощью командлета [Get-Help](https://technet.microsoft.com/en-us/library/hh849696.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb494-106">Users can access the help by calling the configuration function with `-?`, or by using the [Get-Help](https://technet.microsoft.com/en-us/library/hh849696.aspx) cmdlet.</span></span> <span data-ttu-id="fb494-107">Дополнительные сведения о справке на основе комментариев PowerShell см. в разделе [about_Comment_Based_Help](https://technet.microsoft.com/en-us/library/hh847834.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb494-107">For more information about PowerShell comment-based help, see [about_Comment_Based_Help](https://technet.microsoft.com/en-us/library/hh847834.aspx).</span></span>

<span data-ttu-id="fb494-108">В следующем примере показан сценарий, который содержит конфигурацию и справку на основе комментариев для этой конфигурации:</span><span class="sxs-lookup"><span data-stu-id="fb494-108">The following example shows a script that contains a configuration and comment-based help for it:</span></span>

```powershell
<#
.SYNOPSIS
A brief description of the function or script. This keyword can be used only once for each configuration.


.DESCRIPTION
A detailed description of the function or script. This keyword can be used only once for each configuration.


.PARAMETER ComputerName
The description of a parameter. Add a .PARAMETER keyword for each parameter in the function or script syntax.

Type the parameter name on the same line as the .PARAMETER keyword. Type the parameter description on the lines following the .PARAMETER keyword. 
Windows PowerShell interprets all text between the .PARAMETER line and the next keyword or the end of the comment block as part of the parameter description. 
The description can include paragraph breaks.

The Parameter keywords can appear in any order in the comment block, but the function or script syntax determines the order in which the parameters 
(and their descriptions) appear in help topic. To change the order, change the syntax.

.PARAMETER FilePath
Provide a PARAMETER section for each parameter that your script or function accepts.

.EXAMPLE
A sample command that uses the function or script, optionally followed by sample output and a description. Repeat this keyword for each example. If you have multiple examples,
there is no need to number them. PowerShell will number the examples in help text.

.EXAMPLE
This example will be labeled "EXAMPLE 2" when help is displayed to the user.
#>

configuration HelpSample1
{
    param([string]$ComputerName,[string]$FilePath)
    File f
    {
        Contents="Hello World"
        DestinationPath = "c:\Destination.txt"
    }
}
```

## <a name="viewing-configuration-help"></a><span data-ttu-id="fb494-109">Просмотр справки по конфигурации</span><span class="sxs-lookup"><span data-stu-id="fb494-109">Viewing configuration help</span></span>

<span data-ttu-id="fb494-110">Для просмотра справки по конфигурации используйте командлет **Get-Help** с именем функции или введите имя функции и `-?`.</span><span class="sxs-lookup"><span data-stu-id="fb494-110">To view the help for a configuration, use the **Get-Help** cmdlet with the name of the function, or type the name of the function followed by `-?`.</span></span> <span data-ttu-id="fb494-111">Ниже приведены выходные данные предыдущей функции при передаче в **Get-Help**.</span><span class="sxs-lookup"><span data-stu-id="fb494-111">The following is the output of the previous function when passed to **Get-Help**:</span></span>

```powershell
PS C:\> Get-Help HelpSample1

NAME
    HelpSample1
    
SYNOPSIS
    A brief description of the function or script. This keyword can be used only once for each configuration.
    
    
SYNTAX
    HelpSample1 [[-InstanceName] <String>] [[-DependsOn] <String[]>] [[-OutputPath] <String>] [[-ConfigurationData] <Hashtable>] [[-ComputerName] 
    <String>] [[-FilePath] <String>] [<CommonParameters>]
    
    
DESCRIPTION
    A detailed description of the function or script. This keyword can be used only once for each configuration.
    

RELATED LINKS

REMARKS
    To see the examples, type: "get-help HelpSample1 -examples".
    For more information, type: "get-help HelpSample1 -detailed".
    For technical information, type: "get-help HelpSample1 -full".
```

## <a name="see-also"></a><span data-ttu-id="fb494-112">См. также</span><span class="sxs-lookup"><span data-stu-id="fb494-112">See Also</span></span>
* [<span data-ttu-id="fb494-113">Конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="fb494-113">DSC Configurations</span></span>](configurations.md)

