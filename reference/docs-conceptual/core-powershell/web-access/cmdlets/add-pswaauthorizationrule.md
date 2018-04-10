---
description: ''
ms.topic: article
ms.prod: powershell
keywords: powershell,командлет
ms.date: 12/12/2016
title: добавление pswaauthorizationrule
ms.technology: powershell
schema: 2.0.0
ms.openlocfilehash: 07ddd4df6a776f3ef6763242f8682747b9b97061
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="add-pswaauthorizationrule"></a>Add-PswaAuthorizationRule

## <a name="synopsis"></a>КРАТКИЙ ОБЗОР

Добавляет новое правило авторизации в набор правил авторизации Windows PowerShell® Web Access.

## <a name="syntax"></a>Синтаксис

### <a name="usergroupnamecomputergroupname"></a>UserGroupNameComputerGroupName
```
Add-PswaAuthorizationRule -ComputerGroupName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usergroupnamecomputername"></a>UserGroupNameComputerName
```
Add-PswaAuthorizationRule -ComputerName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputergroupname"></a>UserNameComputerGroupName
```
Add-PswaAuthorizationRule [-UserName] <String[]> -ComputerGroupName <String> -ConfigurationName <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputername"></a>UserNameComputerName
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
Дополнительные сведения см. в разделе [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).

## <a name="inputs"></a>ВХОДНЫЕ ДАННЫЕ

### <a name="string"></a>Строка

Этот командлет принимает в качестве входных данных строку или массив строк.

### <a name="string"></a>String\[\]

Этот командлет принимает в качестве входных данных строку или массив строк.

## <a name="outputs"></a>Выходные данные

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule

Этот командлет возвращает объект правила авторизации.

## <a name="examples"></a>ПРИМЕРЫ

### <a name="example-1"></a>ПРИМЕР 1

В этом примере предоставляется доступ к конфигурации сеанса *PSWAEndpoint*, ограниченному пространству выполнения, на сервере *srv2* для пользователей в группе *SMAdmins*.
**Примечание**. Имя компьютера должно указываться в виде полного доменного имени. Администраторы определяют ограниченную конфигурацию сеанса или пространства выполнения, то есть ограниченный набор командлетов и задач, которые могут выполнять конечные пользователи. Определение ограниченного пространства выполнения блокирует доступ пользователей к другим компьютерам, которые находятся за пределами разрешенного пространства выполнения Windows PowerShell®, тем самым обеспечивая более безопасное подключение. Дополнительные сведения о конфигурациях сеансов см. в разделе [about_Session_Configurations](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) или [Установка и использование Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).

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

````PowerShell
$o = New-Object -TypeName PSObject |
    Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru |
    Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru |
    Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" –PassThru

$o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell
````

### <a name="example-5"></a>ПРИМЕР 5

В этом примере добавляется правило, которое предоставляет локальному пользователю с именем *PswaServer\\ChrisLocal* доступ к серверу с именем *srv1.contoso.com*.

В этом примере показана ситуация, в которой шлюз находится в рабочей группе, а целевой компьютер входит в домен. Правило авторизации применяется к локальным пользователям на сервере шлюза. На странице входа Windows PowerShell Web Access для успешного прохождения проверки подлинности пользователь должен предоставить второй набор учетных данных в области **Дополнительные параметры подключения**. Сервер шлюза использует этот дополнительный набор учетных данных для проверки подлинности пользователя на конечном компьютере (сервере *srv1.contoso.com*).

````
Add-PswaAuthorizationRule –UserName PswaServer\ChrisLocal –ComputerName srv1.contoso.com –ConfigurationName Microsoft.PowerShell
````

### <a name="example-6"></a>ПРИМЕР 6

В этом примере всем пользователям предоставляется доступ ко всем конечным точкам на всех компьютерах.
Это по сути отключает правила авторизации.
**Примечание**. Использование подстановочного знака `*` не рекомендуется для конфиденциальных развертываний и может использоваться только в тестовых средах или развертываниях с невысокими требованиями к безопасности.

````PowerShell
Add-PswaAuthorizationRule –UserName * -ComputerName * -ConfigurationName *
````

## <a name="see-also"></a>См. также

- [Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)
- [Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)
- [Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)
- [Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)
- [Add-Member](http://go.microsoft.com/fwlink/p/?LinkId=113280)
- [New-Object](http://go.microsoft.com/fwlink/p/?LinkId=113355)
- [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936)