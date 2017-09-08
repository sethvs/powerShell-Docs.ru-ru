---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "добавление pswaauthorizationrule"
ms.technology: powershell
schema: 2.0.0
ms.openlocfilehash: 12f5cc30d4e3f9cfdd739cacbbab96134077e50a
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2017
---
#  <a name="add-pswaauthorizationrule"></a>Add-PswaAuthorizationRule

##  <a name="synopsis"></a>КРАТКИЙ ОБЗОР

Добавляет новое правило авторизации в набор правил авторизации Windows PowerShell® Web Access.

## <a name="syntax"></a>Синтаксис

###  <a name="usergroupnamecomputergroupname"></a>UserGroupNameComputerGroupName
```
Add-PswaAuthorizationRule -ComputerGroupName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

###  <a name="usergroupnamecomputername"></a>UserGroupNameComputerName
```
Add-PswaAuthorizationRule -ComputerName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

###  <a name="usernamecomputergroupname"></a>UserNameComputerGroupName
```
Add-PswaAuthorizationRule [-UserName] <String[]> -ComputerGroupName <String> -ConfigurationName <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

###  <a name="usernamecomputername"></a>UserNameComputerName
```
Add-PswaAuthorizationRule [-UserName] <String[]> [-ComputerName] <String> [-ConfigurationName] <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

## <a name="description"></a>ОПИСАНИЕ

Командлет **Add-PswaAuthorizationRule** добавляет новое правило авторизации в набор правил авторизации Windows PowerShell® Web Access.

Для этого правила необходимо указать пользователей, компьютеры и конечные точки Windows PowerShell. Можно указать пользователей и компьютеры по отдельности (имена учетных записей и имена компьютеров) или задать группу.

Чтобы создать правило для компьютера, который присоединен к домену Active Directory, командлет использует идентификатор безопасности (SID) этого компьютера.
Это позволяет указать в поле **Имя компьютера** на странице входа короткое имя, полное доменное имя или IP-адрес.

Для компьютера, который не присоединен к домену Active Directory, командлет создает правило, используя имя компьютера, предоставленное администратором. Для успешного подключения к этому компьютеру конечному пользователю необходимо указать имя компьютера точно так, как оно отображается в правиле.

При наличии в сети нескольких компьютеров с одним именем короткое имя можно разрешить в несколько компьютеров. Это может привести к неоднозначности при установке подключения. Например, если правило существует для компьютера рабочей группы с именем *Server1* и к сети подключается новый компьютер с именем *server1.contoso.com*, проверка с помощью правил авторизации выполняется успешно и Windows PowerShell Web Access пытается установить подключение к компьютеру с именем *Server1*. Но нет никакой гарантии, что подключение будет установлено с указанным компьютером рабочей группы: попытка будет выполняться как для компьютера в рабочей группе, так и для компьютера домена с именем *Server1*. Чтобы избежать неоднозначности, для создания правил авторизации рекомендуется по возможности использовать полное доменное имя целевого компьютера.

Правила авторизации проверяют основные учетные данные пользователей Windows PowerShell Web Access, а не альтернативные учетные данные (второй набор учетных данных содержится в разделе **Дополнительные параметры подключения** на странице входа). Дополнительные сведения см. в примере 6.

## <a name="parameters"></a>Параметры

### <a name="-computergroupnameltstringgt"></a>-ComputerGroupName&lt;строка&gt;

Указывает имя группы компьютеров в доменных службах Active Directory (AD DS) или локальных группах, к которым это правило предоставляет доступ.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | верно                                 |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | True (ByPropertyName)                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-computernameltstringgt"></a>-ComputerName&lt;строка&gt;

Указывает имя компьютера, к которому это правило предоставляет доступ.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | верно                                 |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | True (ByPropertyName)                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-configurationnameltstringgt"></a>-ConfigurationName&lt;строка&gt;

Указывает имя конфигурации сеанса Windows PowerShell (также известной как пространство выполнения), к которой это правило предоставляет доступ.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | верно                                 |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | True (ByPropertyName)                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-credentialltpscredentialgt"></a>-Credential&lt;PSCredential&gt;

Указывает объект **PSCredential** для учетной записи пользователя, который предполагается использовать для изменения правил авторизации Windows PowerShell Web Access. Если этот параметр не добавлен, командлет будет использовать учетную запись текущего пользователя. Чтобы получить объект **PSCredential**, который требуется для удаленного добавления правил авторизации, запустите командлет [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-force"></a>-Force

Принудительное выполнение команды без запроса на подтверждение пользователем.
Кроме того, выводится запрос на подтверждение при вводе простого или короткого имени компьютера (например, имени, которое не является именем домена или указано не полностью). Подтверждение запрашивается из соображений безопасности, чтобы простое имя можно было использовать для добавления компьютера только в том случае, если компьютер входит в рабочую группу.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-rulenameltstringgt"></a>-RuleName&lt;строка&gt;

Задает понятное имя для этого правила.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | True (ByPropertyName)                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-usergroupnameltstringgt"></a>-UserGroupName&lt;строка\[\]&gt;

Указывает имя одной или нескольких групп пользователей в AD DS или локальных группах, к которым это правило предоставляет доступ.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | верно                                 |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | True (ByPropertyName)                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-usernameltstringgt"></a>-UserName&lt;строка\[\]&gt;

Указывает одного или нескольких пользователей, к которым это правило предоставляет доступ. Имя пользователя может быть локальной учетной записью пользователя на компьютере шлюза или пользователем в доменных службах Active Directory.
Формат: `domain\user` или `computer\user`.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | верно                                 |
| Указать положение?                            | 1                                    |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | True (ByValue, ByPropertyName)       |
| Принимать подстановочные знаки?          | false                                |

### <a name="ltcommonparametersgt"></a>&lt;CommonParameters&gt;

Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.
Дополнительные сведения см. в разделе [about_CommonParameters](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).

## <a name="inputs"></a>ВХОДНЫЕ ДАННЫЕ

###  <a name="string"></a>Строка

Этот командлет принимает в качестве входных данных строку или массив строк.

###  <a name="string"></a>String\[\]

Этот командлет принимает в качестве входных данных строку или массив строк.

##  <a name="outputs"></a>Выходные данные

###   <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule

Этот командлет возвращает объект правила авторизации.

## <a name="examples"></a>ПРИМЕРЫ

### <a name="example-1"></a>ПРИМЕР 1

В этом примере предоставляется доступ к конфигурации сеанса *PSWAEndpoint*, ограниченному пространству выполнения, на сервере *srv2* для пользователей в группе *SMAdmins*.
**Примечание**. Имя компьютера должно указываться в виде полного доменного имени. Администраторы определяют ограниченную конфигурацию сеанса или пространства выполнения, то есть ограниченный набор командлетов и задач, которые могут выполнять конечные пользователи. Определение ограниченного пространства выполнения блокирует доступ пользователей к другим компьютерам, которые находятся за пределами разрешенного пространства выполнения Windows PowerShell®, тем самым обеспечивая более безопасное подключение. Дополнительные сведения о конфигурациях сеансов см. в разделе [about_Session_Configurations](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) или [Установка и использование Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).

```PowerShell
Add-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserGroupName contoso\SMAdmins -ConfigurationName PSWAEndpoint
```

### <a name="example-2"></a>ПРИМЕР 2

В этом примере предоставляется доступ к конфигурации сеанса Windows PowerShell по умолчанию, `Microsoft.PowerShell` на сервере *srv2* для пользователей с именем contoso\\user1, contoso\\user2 и contoso\\user3. Этот командлет создает три правила (по одному на каждого человека).

```PowerShell
Add-PswaAuthorizationRule –UserName contoso\user1, contoso\user2, contoso\user3 –ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-3"></a>ПРИМЕР 3

В этом примере показано, как вводить значения имен пользователей через конвейер.

```
"contoso\user1","contoso\user2" | Add-pswaAuthorizationRule –ComputerName srv2.contoso.com –ConfigurationName Microsoft.PowerShell
```

### <a name="example-4"></a>ПРИМЕР 4

В этом примере показано, как все параметры принимают значения из конвейера по имени свойства.

\
###   <a name="section-subheading"></a>{#section .subHeading}

<div class="subSection">

<div id="code-snippet-5" class="codeSnippetContainer" xmlns="">

<div class="codeSnippetContainerTabs">

<div class="codeSnippetContainerTabSingle" dir="ltr">

[Windows PowerShell]()

</div>

</div>

<div class="codeSnippetContainerCodeContainer">

<div class="codeSnippetToolBar">

<div class="codeSnippetToolBarText">

[Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_b61200ba-32cd-4df3-80be-7d5cf0ff709f'); "Копировать в буфер обмена.")

</div>

</div>

<div id="CodeSnippetContainerCode_b61200ba-32cd-4df3-80be-7d5cf0ff709f"
class="codeSnippetContainerCode" dir="ltr">

<div style="color:Black;">

    PS C:\> $o = New-Object -TypeName PSObject | Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru | Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru | Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" –PassThru

</div>

</div>

</div>

</div>

</div>

###   <a name="section-1-subheading"></a>{#section-1 .subHeading}

<div class="subSection">

<div id="code-snippet-6" class="codeSnippetContainer" xmlns="">

<div class="codeSnippetContainerTabs">

<div class="codeSnippetContainerTabSingle" dir="ltr">

[Windows PowerShell]()

</div>

</div>

<div class="codeSnippetContainerCodeContainer">

<div class="codeSnippetToolBar">

<div class="codeSnippetToolBarText">

[Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_c76e1b6c-cb67-4223-a7d0-54ec6b63bbcb'); "Копировать в буфер обмена.")

</div>

</div>

<div id="CodeSnippetContainerCode_c76e1b6c-cb67-4223-a7d0-54ec6b63bbcb"
class="codeSnippetContainerCode" dir="ltr">

<div style="color:Black;">

    PS C:\> $o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell

</div>

</div>

</div>

</div>

</div>

</div>

### <a name="example-5-example-5-subheading"></a>ПРИМЕР 5 {#example-5 .subHeading}

<div class="subSection">

В этом примере добавляется правило, которое предоставляет локальному пользователю с именем *PswaServer\\ChrisLocal* доступ к серверу с именем *srv1.contoso.com*.

В этом примере показана ситуация, в которой шлюз находится в рабочей группе, а целевой компьютер входит в домен. Правило авторизации применяется к локальным пользователям на сервере шлюза. На странице входа Windows PowerShell Web Access для успешного прохождения проверки подлинности пользователь должен предоставить второй набор учетных данных в области **Дополнительные параметры подключения**. Сервер шлюза использует этот дополнительный набор учетных данных для проверки подлинности пользователя на конечном компьютере (сервере *srv1.contoso.com*).

\
<div id="code-snippet-7" class="codeSnippetContainer" xmlns="">

<div class="codeSnippetContainerTabs">

<div class="codeSnippetContainerTabSingle" dir="ltr">

[Windows PowerShell]()

</div>

</div>

<div class="codeSnippetContainerCodeContainer">

<div class="codeSnippetToolBar">

<div class="codeSnippetToolBarText">

[Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_7572cdeb-8835-49ed-9d8e-d3318eb639d3'); "Копировать в буфер обмена.")

</div>

</div>

<div id="CodeSnippetContainerCode_7572cdeb-8835-49ed-9d8e-d3318eb639d3"
class="codeSnippetContainerCode" dir="ltr">

<div style="color:Black;">

    PS C:\> Add-PswaAuthorizationRule –UserName PswaServer\ChrisLocal –ComputerName srv1.contoso.com –ConfigurationName Microsoft.PowerShell

</div>

</div>

</div>

</div>

</div>

### <a name="example-6-example-6-subheading"></a>ПРИМЕР 6 {#example-6 .subHeading}

<div class="subSection">

В этом примере всем пользователям предоставляется доступ ко всем конечным точкам на всех компьютерах.
Это по сути отключает правила авторизации.
**Примечание**. Использование подстановочного знака `*` не рекомендуется для конфиденциальных развертываний и может использоваться только в тестовых средах или развертываниях с невысокими требованиями к безопасности.

\
<div id="code-snippet-8" class="codeSnippetContainer" xmlns="">

<div class="codeSnippetContainerTabs">

<div class="codeSnippetContainerTabSingle" dir="ltr">

[Windows PowerShell]()

</div>

</div>

<div class="codeSnippetContainerCodeContainer">

<div class="codeSnippetToolBar">

<div class="codeSnippetToolBarText">

[Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_9fb751ca-1e50-4411-a9a9-3343fe888076'); "Копировать в буфер обмена.")

</div>

</div>

<div id="CodeSnippetContainerCode_9fb751ca-1e50-4411-a9a9-3343fe888076"
class="codeSnippetContainerCode" dir="ltr">

<div style="color:Black;">

    PS C:\> Add-PswaAuthorizationRule –UserName * -ComputerName * -ConfigurationName *

</div>

</div>

</div>

</div>

</div>

</div>

<a name="related-topics"></a>Связанные темы 
--------------


[Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)\
\
[Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)\
\
[Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)\
\
[Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)\
\
[Add-Member](http://go.microsoft.com/fwlink/p/?LinkId=113280)\
\
[New-Object](http://go.microsoft.com/fwlink/p/?LinkId=113355)\
\
[Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936)