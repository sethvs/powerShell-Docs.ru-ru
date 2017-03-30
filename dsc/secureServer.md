---
title: "Рекомендации по опрашивающим серверам"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: carmonm
ms.prod: powershell
ms.openlocfilehash: af86f1f93a1035ec52a8b029acdd826e8463e2c2
ms.sourcegitcommit: ba8ed836799ef465e507fa1b8d341ba38459d863
translationtype: HT
---
# <a name="pull-server-best-practices"></a>Рекомендации по опрашивающим серверам

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Аннотация. В данном документе описываются процессы и действия, которые могут быть полезны для инженеров, готовящихся к развертыванию решения. Информация в документе содержит в себе рекомендации, изложенные клиентами и затем проверенные рабочей группой по продукту, что позволяет гарантировать их перспективность и стабильность.

| |Информация о документе|
|:---|:---|
Дизайнер | Майкл Грин (Michael Greene)  
Рецензенты | Бен Геленс (Ben Gelens), Равикант Чаганти (Ravikanth Chaganti), Александар Николич (Aleksandar Nikolic)  
Опубликован | Апрель 2015 г.

## <a name="abstract"></a>Аннотация

В этом документе приводятся официальные рекомендации для специалистов, планирующих внедрить опрашивающий сервер настройки требуемого состояния Windows PowerShell. Опрашивающий сервер представляет собой простую службу, которая должна развертываться за минуты. Несмотря на то, что в этом документе и представлены технические практические инструкции по развертыванию, он ценен прежде всего тем, что является своего рода справочником с рекомендациями и советами относительно важных моментов, которые необходимо принимать во внимание перед развертыванием.
Читатели должны иметь общее представление о DSC и понимать термины, используемые для описания компонентов, входящих в развертывание DSC. Дополнительные сведения см. в статье [Общие сведения о службе настройки требуемого состояния Windows PowerShell](https://technet.microsoft.com/en-us/library/dn249912.aspx).
Поскольку предполагается, что темп развития DSC соответствует скорости совершенствования облачных служб, можно ожидать, что базовая технология, включая опрашивающий сервер, также будет эволюционировать и давать новые возможности. В приложении к этому документу содержится таблица версий со ссылками на предыдущие выпуски и будущие решения для стимулирования разработки проектов с заделом на будущее.

Этот документ состоит из двух основных разделов:

 - Планирование настройки
 - Руководство по установке
 
### <a name="versions-of-the-windows-management-framework"></a>Версии Windows Management Framework 
Информация в этом документе рассчитана на Windows Management Framework 5.0. И хотя для развертывания и эксплуатации опрашивающего сервера WMF 5.0 и не требуется, акцент в этом документе сделан именно на версии 5.0.

### <a name="windows-powershell-desired-state-configuration"></a>Настройка необходимого состояния Windows PowerShell
Настройка требуемого состояния (DSC) — это платформа управления для развертывания данных конфигурации и управления ими при помощи отраслевого синтаксиса Managed Object Format (MOF) для описания модели Common Information Model (CIM). Для дальнейшей разработки этих стандартов на платформах, включая Linux и операционные системы для сетевого оборудования, существует проект с открытым исходным кодом — открытая инфраструктура управления (Open Management Infrastructure, OMI). Дополнительные сведения см. на [странице DMTF со спецификациями MOF](http://dmtf.org/standards/cim) и в [документах по OMI](https://collaboration.opengroup.org/omi/documents.php).

Windows PowerShell предоставляет набор расширений языка для настройки требуемого состояния, который можно использовать для создания декларативных конфигураций и управления ими.

### <a name="pull-server-role"></a>Роль опрашивающего сервера  
Опрашивающий сервер является централизованной службой для хранения конфигураций, которые будут доступны для целевых узлов.
 
Роль опрашивающего сервера может быть развернута как экземпляр веб-сервера или общая папка SMB. Веб-сервер использует интерфейс OData и при необходимости может включать в себя возможности, позволяющие целевым узлам подтверждать успешное применение конфигураций или сообщать о неудаче. Это полезно в средах с большим числом целевых узлов. После настройки целевого узла (также называемого клиентом) на указание на опрашивающий сервер происходит скачивание и применение последних данных конфигурации и всех необходимых скриптов. Этот процесс может быть реализован как однократное развертывание или как повторно выполняющееся задание, что делает опрашивающий сервер важным активом для управления изменениями на должном уровне. Дополнительные сведения см. в статьях [Настройка опрашивающего веб-сервера DSC](https://technet.microsoft.com/en-us/library/dn249913.aspx) и [Push and Pull Configuration Modes](https://technet.microsoft.com/en-us/library/dn249913.aspx) (Режимы конфигурации Push и Pull).

## <a name="configuration-planning"></a>Планирование настройки

В рамках любого развертывания программного обеспечения в организации существует информация, которую можно собрать заранее, чтобы спланировать нужную архитектуру и подготовиться к этапам, необходимым для выполнения развертывания. В следующих разделах приводится информация о подготовке и подключениях, которые, скорее всего, потребуется реализовать заблаговременно.

### <a name="software-requirements"></a>Требования к программному обеспечению

Для развертывания опрашивающего сервера требуется служба DSC сервера Windows Server. Этот компонент появился в Windows Server 2012 и обновлялся в рамках текущих выпусков Windows Management Framework (WMF).

### <a name="software-downloads"></a>Файлы программного обеспечения для скачивания

Помимо установки последнего содержимого из Центра обновления Windows следует скачать два компонента, рекомендуемых для развертывания опрашивающего сервера DSC: последнюю версию Windows Management Framework и модуль DSC для автоматизированной подготовки опрашивающего сервера.

### <a name="wmf"></a>WMF

В состав Windows Server 2012 R2 входит компонент, который называется службой DSC. Служба DSC обеспечивает функциональность опрашивающего сервера, включая предоставление двоичных файлов, которые поддерживают конечную точку OData. WMF является частью Windows Server и регулярно обновляется между выпусками Windows Server. [Новые версии WMF 5.0](http://aka.ms/wmf5latest) могут содержать обновления для службы DSC. Поэтому рекомендуется скачать последний выпуск WMF и ознакомиться с заметками о нем, чтобы узнать, есть ли обновление для службы DSC. Кроме того, в заметках о выпуске следует просмотреть раздел, где указано состояние обновления или сценария (стабильный выпуск или экспериментальный). Чтобы реализовать гибкий цикл выпуска, отдельные компоненты могут быть объявлены стабильными, что говорит об их готовности к использованию в рабочей среде даже в том случае, если выпущена лишь предварительная версия WMF.
Другие компоненты, которые исторически обновлялись в выпусках WMF (подробности см. в заметках о выпуске WMF):

 - Windows PowerShell, интегрированная среда скриптов Windows PowerShell (ISE).
 - Веб-службы Windows PowerShell (расширение IIS OData для управления).
 - Настройка требуемого состояния Windows PowerShell (DSC).
 - Удаленное управление Windows (WinRM), инструментарий управления Windows (WinRM).

### <a name="dsc-resource"></a>Ресурс DSC

Развертывание опрашивающего сервера можно упростить, подготовив службу с использованием скрипта настройки DSC. В этот документ включены скрипты настройки, которые можно использовать для развертывания узла сервера, готового к внедрению в рабочую среду. Для использования скриптов настройки требуется модуль DSC, не входящий в состав Windows Server. Название модуля — **xPSDesiredStateConfiguration**; модуль содержит ресурс DSC **xDscWebService**. Модуль xPSDesiredStateConfiguration можно скачать [здесь](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).

Используйте командлет **Install-Module** из модуля **PowerShellGet**.

```powershell
Install-Module xPSDesiredStateConfiguration
```

Модуль **PowerShellGet** скачает модуль в следующую папку: 

`C:\Program Files\Windows PowerShell\Modules`

Задача по планированию|
---|
Есть ли у вас доступ к установочным файлам Windows Server 2012 R2?|
Будет ли у среды развертывания доступ к Интернету для скачивания WMF и модуля из коллекции в сети?|
Каким образом будут установлены последние обновления для системы безопасности после установки операционной системы?|
Будет ли у среды доступ к Интернету для получения обновлений или же в ней будет размещен локальный сервер с Windows Server Update Services (WSUS)?|
Есть ли у вас доступ к установочным файлам Windows Server, уже содержащим обновления, добавленные посредством вставки?|

### <a name="hardware-requirements"></a>Требования к оборудованию

Развертывания опрашивающих серверов поддерживаются как на физических, так и виртуальных серверах. Требования к размеру для опрашивающего сервера соответствуют требованиям Windows Server 2012 R2.

Процессор: 64-разрядный процессор с тактовой частотой 1,4 ГГц.  
Память: 512 МБ.  
Место на диске: 32 ГБ.  
Сеть: адаптер Gigabit Ethernet.  

Задача по планированию|
---|
Развертывание будет выполняться на физическом оборудовании или платформе виртуализации?|
В чем заключается процесс запроса нового сервера для целевой среды?|
Каково среднее время получения доступа к серверу?|
Сервер какого размера будет запрошен?|

### <a name="accounts"></a>Учетные записи

Требования, связанные с учетными записями служб, для развертывания экземпляра опрашивающего сервера отсутствуют. Однако в некоторых случаях веб-сайт может работать в контексте учетной записи локального пользователя. Например, иногда необходимо получить доступ к общей папке хранилища с содержимым веб-сайта, а сервер Windows Server или устройство, на котором размещена общая папка хранилища, не присоединены к домену.

### <a name="dns-records"></a>Записи DNS

При настройке клиентов для работы в среде опрашивающего сервера вам потребуется название сервера. В тестовой среде обычно используется имя узла сервера, а если разрешение имен DNS недоступно, можно использовать IP-адрес сервера. В рабочих средах или в лабораторной среде, предназначенной для представления рабочего развертывания, рекомендуется создать запись DNS CNAME.

Запись DNS CNAME позволяет сформировать псевдоним для ссылки на запись узла (A). Дополнительная запись имени предназначена для повышения гибкости, если в будущем потребуется вносить изменения. Запись CNAME помогает изолировать конфигурацию клиента, чтобы в случае внесения изменений в серверную среду (например, замена опрашивающего сервера или добавление дополнительных опрашивающих серверов), не потребовалось изменять конфигурацию клиента соответствующим образом.

При выборе названия для записи DNS следует учитывать архитектуру решения. Если используется балансировка нагрузки, название сертификата, применяемого для защиты трафика по протоколу HTTPS, должно совпадать с названием записи DNS. 

Сценарий |Рекомендация
:---|:---
Тестовая среда |По возможности воспроизведите запланированную рабочую среду. Для простых конфигураций подойдет имя узла сервера. Если служба DNS недоступна, вместо имени узла можно использовать IP-адрес.|
Развертывание одного узла |Создайте запись DNS CNAME, которая указывает на имя узла сервера.|

Дополнительные сведения см. в статье [Configuring DNS Round Robin in Windows Server](https://technet.microsoft.com/en-us/library/cc787484(v=ws.10).aspx) (Настройка циклического перебора DNS в Windows Server).

Задача по планированию|
---|
Вы знаете, к кому обращаться по вопросам создания и изменения записей DNS?|
Каково среднее время обработки запроса, связанного с записью DNS?|
Вам требуется запрашивать статические записи имени узла (A) для серверов?|
Что вы будете запрашивать в качестве CNAME?|
Какой тип решения по балансировке нагрузки вы будете использовать в случае необходимости? (Дополнительные сведения см. в разделе о балансировке нагрузки.)|

### <a name="public-key-infrastructure"></a>Инфраструктура открытых ключей

Большинству современных организаций требуется проверка и шифрование передаваемого сетевого трафика и, в частности, трафика, содержащего конфиденциальные данные о конфигурации серверов. Несмотря на то, что опрашивающий сервер можно развернуть с использованием протокола HTTP, что облегчает обработку запросов от клиентов (так как используется открытый текст), рекомендуется защитить трафик при помощи протокола HTTPS. Службу можно настроить на использование HTTPS, применив набор параметров в ресурсе DSC **xPSDesiredStateConfiguration**.

Требования, касающиеся сертификатов, для защиты трафика HTTPS опрашивающего сервера аналогичны требованиям, применимым к защите любого другого веб-сайта с HTTPS. Шаблон **веб-сервера** в службах сертификации Windows Server удовлетворяет необходимым условиям.

Задача по планированию|
---|
К кому потребуется обратиться для получения сертификата (если запросы на сертификаты не обрабатываются автоматически)?|
Каково среднее время обработки запроса?|
Каким образом вам будет передан файл сертификата?|
Каким образом вам будет передан закрытый ключ сертификата?|
Каков срок действия по умолчанию?|
Вы выбрали имя DNS для среды опрашивающего сервера, которое можно использовать в названии сертификата?|

### <a name="choosing-an-architecture"></a>Выбор архитектуры

Опрашивающий сервер можно развернуть при помощи веб-службы, размещенной в службах IIS, или общей папки SMB. В большинстве случаев вариант с использованием веб-службы обеспечит большую гибкость. Как правило, трафик HTTPS проходит через границы сети, тогда как трафик SMB часто отфильтровывается или блокируется между сетями. Веб-служба предусматривает возможность включения Conformance Server или диспетчера веб-отчетов (Web Reporting Manager) (оба компонента будут рассматриваться в будущей версии этого документа), которые предоставляют для клиентов механизм сообщения о состоянии на сервер в целях централизованного контроля. SMB подходит для использования в средах, где политика запрещает эксплуатацию веб-сервера, и в других ситуациях, когда применение роли веб-сервера является нежелательным. Вне зависимости от выбранного варианта не забудьте оценить требования, касающиеся подписывания и шифрования трафика. Стоит принять во внимание такие моменты, как передача трафика HTTPS, подписывание SMB и политики IPSEC.

#### <a name="load-balancing"></a>Балансировка нагрузки  
Клиенты, взаимодействующие с веб-службой, направляют запрос на получение данных, возвращаемых в одном ответе. Последующие запросы не нужны, поэтому платформе балансировки нагрузки не требуется обеспечивать постоянную поддержку сеансов на одном сервере.

Задача по планированию|
---|
Какое решение будет использоваться для балансировки нагрузки трафика между серверами?|
Кто выполнит запрос на добавление новой конфигурации на устройство в случае использования аппаратной подсистемы балансировки нагрузки?|
Каково среднее время обработки запроса на настройку новой веб-службы с балансировкой нагрузки?|
Какие данные будут необходимы для запроса?|
Запрашивать дополнительный IP-адрес будете вы или рабочая группа, ответственная за балансировку нагрузки?|
Есть ли у вас необходимые записи DNS? Потребуются ли они рабочей группе, отвечающей за настройку решения по балансировке нагрузки?|
Нужно ли, чтобы в решении по балансировке нагрузки обработку PKI выполняло устройство? Или балансировка нагрузки трафика HTTPS может осуществляться до тех пор, пока отсутствуют требования, связанные сеансами?|

### <a name="staging-configurations-and-modules-on-the-pull-server"></a>Промежуточные конфигурации и модули на опрашивающем сервере

При планировании конфигурации необходимо подумать о том, какие модули DSC и конфигурации будут размещены на опрашивающем сервере. Кроме того, важно иметь базовые знания о принципах развертывания содержимого на опрашивающем сервере и подготовки к этому процессу. 

В будущем этот раздел будет расширен и включен в руководство по эксплуатации опрашивающего сервера DSC.  В руководстве будет рассматриваться рутинный процесс управления модулями и конфигурациями с применением автоматизации. 

#### <a name="dsc-modules"></a>Модули DSC  
Клиентам, запрашивающим конфигурацию, потребуются некоторые модули DSC. Функциональность опрашивающего сервера заключается в автоматизации распространения модулей DSC на клиенты по запросу. При первом развертывании опрашивающего сервера (возможно, для проверки концепции или в тестовой среде) вы, скорее всего, будете зависеть от модулей DSC из общедоступных репозиториев, таких как коллекция PowerShell или репозитории PowerShell.org на сайте GitHub.

Важно помнить, что даже при использовании надежных сетевых источников, таких как коллекция PowerShell, любой модуль, скачиваемый из общедоступного репозитория, должен быть проверен специалистом с опытом работы с PowerShell и знаниями о среде, где будут использоваться модули, прежде чем они будут внедрены в рабочие условия. При выполнении этой задачи рекомендуется проверить наличие в модуле дополнительных полезных данных, которые можно удалить, например документацию и скрипты-примеры. Это позволит снизить долю полосы пропускания, используемую каждым клиентом при первом запросе, когда будет выполняться скачивание модулей с сервера на клиент по сети.

Каждый модуль должны быть упакован в определенном формате — это должен быть ZIP-файл с названием в формате "Название_модуля_Версия.zip", который содержит полезные данные модуля. После копирования файла на сервер необходимо создать файл контрольной суммы. При подключении клиентов к серверу контрольная сумма используется для проверки неизменности содержимого модуля DSC с момента его публикации.

```powershell
New-DscCheckSum -ConfigurationPath .\ -OutPath .\
```

Задача по планированию|
---|
Какие ключевые ситуации следует проверить при планировании реализации тестовой или лабораторной среды?|
Существуют ли общедоступные модули, которые содержат ресурсы, охватывающие все, что вам нужно, или вам потребуется создать собственные ресурсы?|
Будет ли у вашей среды доступ к Интернету для получения общедоступных модулей?|
Кто будет отвечать за проверку модулей DSC?|
Если вы планируете производственную среду, что вы будете использовать в качестве локального репозитория для хранения модулей DSC?|
Будет ли центральная рабочая группа принимать модули DSC от рабочих групп по разработке приложений? В чем будет заключаться процесс?|
Будут ли автоматизированы процессы упаковки, копирования и создания контрольной суммы для модулей DSC, готовых к развертыванию на сервере в рабочей среде, из исходного репозитория?|
Будет ли ваша рабочая группа отвечать за управление платформой автоматизации?|

#### <a name="dsc-configurations"></a>Конфигурации DSC

Опрашивающий сервер предназначен для предоставления централизованного механизма для распределения конфигураций DSC на клиентские узлы. Конфигурации хранятся на сервере в виде документов MOF. Каждый документ получит название с уникальным идентификатором GUID. В ходе настройки клиентов на подключение к опрашивающему серверу им также назначается идентификатор GUID конфигурации, которую они должны запросить. Эта система ссылок на конфигурации по идентификатору GUID гарантирует глобальную уникальность и является гибкой, поэтому конфигурация может применяться детализировано для каждого узла или в виде конфигурации роли, охватывающей несколько серверов, которые должны иметь одинаковые настройки.

#### <a name="guids"></a>Идентификаторы GUID

Продумывая нюансы развертывания опрашивающего сервера, рекомендуется уделить особое внимание вопросу планирования реализации идентификаторов GUID в конфигурации. Особые требования к обработке идентификаторов GUID отсутствуют, и процесс,скорее всего, будет уникален и зависеть от конкретной среды. Он может быть простым или же весьма сложным: централизованно хранимый CSV-файл, простая таблица SQL, база данных управления конфигурацией (CMDB), либо сложное решение, требующее интеграции с другим инструментом или программным решением. Существует два общих подхода, описанных далее.

 - **Назначение идентификаторов GUID каждому серверу** — гарантируется, что конфигурация каждого сервера управляется отдельно. Этот вариант обеспечивает определенный уровень точности, когда речь идет об обновлениях, и хорошо подходит для сред с небольшим числом серверов.
 - **Назначение идентификаторов GUID каждой роли сервера** — все серверы, которые выполняют одну и ту же функцию, например веб-серверы, используют один и тот же идентификатор GUID для ссылки на необходимые данные конфигурации.  Необходимо иметь в виду, что если идентификатор GUID является общим для множества серверов, все они будут обновлены одновременно в случае изменения конфигурации.

Идентификатор GUID следует воспринимать как конфиденциальные данные, так как злоумышленники могут использовать его для получения данных о развертывании и настройке серверов в вашей среде. Дополнительные сведения см. в статье [Securely allocating GUIDs in PowerShell Desired State Configuration Pull Mode](http://blogs.msdn.com/b/powershell/archive/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode.aspx) (Безопасное выделение идентификаторов GUID в режиме запроса настройки требуемого состояния в PowerShell).

Задача по планированию|
---|
Кто будет отвечать за копирование готовых конфигураций в папку опрашивающего сервера?|
В чем будет заключаться процесс передачи конфигураций, создаваемых рабочей группой по разработке приложений?|
Будете ли вы использовать репозиторий для хранения создаваемых группами конфигураций?|
Будет ли автоматизирован процесс копирования готовых конфигураций на сервер и создания контрольной суммы?|
Как будут сопоставляться идентификаторы GUID с серверами или ролями и где они будут храниться?|
В чем будет заключаться процесс настройки клиентских компьютеров и каким образом он будет интегрирован с процессом создания и хранения идентификаторов GUID конфигурации?|

## <a name="installation-guide"></a>Руководство по установке

*Скрипты, приведенные в этом документе, относятся к категории стабильного кода. Всегда внимательно проверяйте скрипты перед их использованием в рабочей среде.*

### <a name="prerequisites"></a>Необходимые компоненты

Чтобы проверить версию PowerShell на сервере, используйте следующую команду.

```powershell
$PSVersionTable.PSVersion
```

Если возможно, обновитесь до последней версии Windows Management Framework.
Затем скачайте модуль `xPsDesiredStateConfiguration`, используя следующую команду.


```powershell
Install-Module xPSDesiredStateConfiguration
```

Перед скачиванием команда запросит у вас подтверждение.

### <a name="installation-and-configuration-scripts"></a>Скрипты для установки и настройки
-

Лучшим способом развертывания опрашивающего сервера DSC является использование скрипта настройки DSC. В этом документе представлены скрипты, включающие как основные параметры, применяемые для настройки только веб-службы DSC, так и дополнительные параметры, применяемые для полной настройки Windows Server и веб-службы DSC.

Примечание. Сейчас для работы модуля DSC `xPSDesiredStateConfiguation` требуется, чтобы на сервере использовался английский язык (EN-US).

### <a name="basic-configuration-for-windows-server-2012"></a>Базовая настройка Windows Server 2012
-------------------------------------------
```powershell
# This is a very basic Configuration to deploy a pull server instance in a lab environment on Windows Server 2012.

Configuration PullServer {
Import-DscResource -ModuleName xPSDesiredStateConfiguration

        # Load the Windows Server DSC Service feature
        WindowsFeature DSCServiceFeature
        {
          Ensure = 'Present'
          Name = 'DSC-Service'
        }

        # Use the DSC Resource to simplify deployment of the web service
        xDSCWebService PSDSCPullServer
        {
          Ensure = 'Present'
          EndpointName = 'PSDSCPullServer'
          Port = 8080
          PhysicalPath = "$env:SYSTEMDRIVE\inetpub\wwwroot\PSDSCPullServer"
          CertificateThumbPrint = 'AllowUnencryptedTraffic'
          ModulePath = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
          ConfigurationPath = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
          State = 'Started'
          DependsOn = '[WindowsFeature]DSCServiceFeature'
        }
}
PullServer -OutputPath 'C:\PullServerConfig\'
Start-DscConfiguration -Wait -Force -Verbose -Path 'C:\PullServerConfig\'
```

### <a name="advanced-configuration-for-windows-server-2012-r2"></a>Расширенная настройка Windows Server 2012 R2

```powershell
# This is an advanced Configuration example for Pull Server production deployments on Windows Server 2012 R2.
# Many of the features demonstrated are optional and provided to demonstrate how to adapt the Configuration for multiple scenarios
# Select the needed resources based on the requirements for each environment.
# Optional scenarios include:
#      * Reduce footprint to Server Core
#      * Rename server and join domain
#      * Switch from SSL to TLS for HTTPS
#      * Automatically load certificate from Certificate Authority
#      * Locate Modules and Configuration data on remote SMB share
#      * Manage state of default websites in IIS
    
param (
        [Parameter(Mandatory=$true)] 
        [ValidateNotNullorEmpty()] 
        [System.String] $ServerName,
        [System.String] $DomainName,
        [System.String] $CARootName,
        [System.String] $CAServerFQDN,
        [System.String] $CertSubject,
        [System.String] $SMBShare,
        [Parameter(Mandatory=$true)] 
        [ValidateNotNullorEmpty()] 
        [PsCredential] $Credential
    )
    
Configuration PullServer {
    Import-DscResource -ModuleName xPSDesiredStateConfiguration, xWebAdministration, xCertificate, xComputerManagement
    Node localhost
    {
            
        # Configure the server to automatically corret configuration drift including reboots if needed.
        LocalConfigurationManager
        {
            ConfigurationMode = 'ApplyAndAutoCorrect'
            RebootNodeifNeeded = $node.RebootNodeifNeeded
            CertificateId = $node.Thumbprint
        }
    
        # Remove all GUI interfaces so the server has minimum running footprint.
        WindowsFeature ServerCore
        {
            Ensure = 'Absent'
            Name = 'User-Interfaces-Infra'
        }
    
        # Set the server name and if needed, join a domain. If not joining a domain, remove the DomainName parameter.
        xComputer DomainJoin
        {
            Name = $Node.ServerName
            DomainName = $Node.DomainName
            Credential = $Node.Credential
        }
    
        # The next series of settings disable IIS and enable TLS, for environments where that is required by policy.
        Registry TLS1_2ServerEnabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'
            ValueName = 'Enabled'
            ValueData = 1
            ValueType = 'Dword'
        }
        Registry TLS1_2ServerDisabledByDefault
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'
            ValueName = 'DisabledByDefault'
            ValueData = 0
            ValueType = 'Dword'
        }
        Registry TLS1_2ClientEnabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'
            ValueName = 'Enabled'
            ValueData = 1
            ValueType = 'Dword'
        }
        Registry TLS1_2ClientDisabledByDefault
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'
            ValueName = 'DisabledByDefault'
            ValueData = 0
            ValueType = 'Dword'
        }
        Registry SSL2ServerDisabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server'
            ValueName = 'Enabled'
            ValueData = 0
            ValueType = 'Dword'
        }
    
        # Install the Windows Server DSC Service feature
        WindowsFeature DSCServiceFeature
        {
            Ensure = 'Present'
            Name = 'DSC-Service'
        }
    
        # If using a certificate from a local Active Directory Enterprise Root Certificate Authority, complete a request and install the certificate
        xCertReq SSLCert
        {
            CARootName = $Node.CARootName
            CAServerFQDN = $Node.CAServerFQDN
            Subject = $Node.CertSubject
            AutoRenew = $Node.AutoRenew
            Credential = $Node.Credential
        }
    
        # Use the DSC resource to simplify deployment of the web service.  You might also consider modifying the default port, possibly leveraging port 443 in environments where that is enforced as a standard.
        xDSCWebService PSDSCPullServer
        {
            Ensure = 'Present'
            EndpointName = 'PSDSCPullServer'
            Port = 8080
            PhysicalPath = "$env:SYSTEMDRIVE\inetpub\wwwroot\PSDSCPullServer"
            CertificateThumbPrint = 'CertificateSubject'
            CertificateSubject = $Node.CertSubject
            ModulePath = "$($Node.SMBShare)\DscService\Modules"
            ConfigurationPath = "$($Node.SMBShare)\DscService\Configuration"
            State = 'Started'
            DependsOn = '[WindowsFeature]DSCServiceFeature'
        }
    
        # Validate web config file contains current DB settings
        xWebConfigKeyValue CorrectDBProvider
        { 
            ConfigSection = 'AppSettings'
            Key = 'dbprovider'
            Value = 'System.Data.OleDb'
            WebsitePath = 'IIS:\sites\PSDSCPullServer'
            DependsOn = '[xDSCWebService]PSDSCPullServer'
        }
        xWebConfigKeyValue CorrectDBConnectionStr
        { 
            ConfigSection = 'AppSettings'
            Key = 'dbconnectionstr'
            Value = 'Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Program Files\WindowsPowerShell\DscService\Devices.mdb;'
            WebsitePath = 'IIS:\sites\PSDSCPullServer'
            DependsOn = '[xDSCWebService]PSDSCPullServer'
        }
    
        # Stop the default website
        xWebsite StopDefaultSite  
        { 
            Ensure = 'Present'
            Name = 'Default Web Site'
            State = 'Stopped'
            PhysicalPath = 'C:\inetpub\wwwroot'
            DependsOn = '[WindowsFeature]DSCServiceFeature'
        }
    }
}
$configData = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            ServerName = $ServerName
            DomainName = $DomainName
            CARootName = $CARootName
            CAServerFQDN = $CAServerFQDN
            CertSubject = $CertSubject
            AutoRenew = $true
            SMBShare = $SMBShare
            Credential = $Credential
            RebootNodeifNeeded = $true
            CertificateFile = 'c:\PullServerConfig\Cert.cer'
            Thumbprint = 'B9A39921918B466EB1ADF2509E00F5DECB2EFDA9'
            }
        )
    }
PullServer -ConfigurationData $configData -OutputPath 'C:\PullServerConfig\'
Set-DscLocalConfigurationManager -ComputerName localhost -Path 'C:\PullServerConfig\'
Start-DscConfiguration -Wait -Force -Verbose -Path 'C:\PullServerConfig\'
    
# .\Script.ps1 -ServerName web1 -domainname 'test.pha' -carootname 'test-dc01-ca' -caserverfqdn 'dc01.test.pha' -certsubject 'CN=service.test.pha' -smbshare '\\sofs1.test.pha\share' 
```


### <a name="verify-pull-server-functionality"></a>Проверка работоспособности опрашивающего сервера

```powershell
# This function is meant to simplify a check against a DSC pull server. If you do not use the default service URL, you will need to adjust accordingly.
function Verify-DSCPullServer ($fqdn) {
    ([xml](invoke-webrequest "https://$($fqdn):8080/psdscpullserver.svc" | % Content)).service.workspace.collection.href
}
Verify-DSCPullServer 'INSERT SERVER FQDN' 

Expected Result:
Action
Module
StatusReport
Node
```

### <a name="configure-clients"></a>Настройка клиентов

```powershell
Configuration PullClient {
    param(
    $ID,
    $Server
    )
        LocalConfigurationManager 
                { 
                    ConfigurationID = $ID;
                    RefreshMode = 'PULL';
                    DownloadManagerName = 'WebDownloadManager';
                    RebootNodeIfNeeded = $true;
                    RefreshFrequencyMins = 30;
                    ConfigurationModeFrequencyMins = 15; 
                    ConfigurationMode = 'ApplyAndAutoCorrect';
                    DownloadManagerCustomData = @{ServerUrl = "http://"+$Server+":8080/PSDSCPullServer.svc"; AllowUnsecureConnection = $true}
                }
}
PullClient -ID 'INSERTGUID' -Server 'INSERTSERVER' -Output 'C:\DSCConfig\'
Set-DscLocalConfigurationManager -ComputerName 'Localhost' -Path 'C:\DSCConfig\' -Verbose
```


## <a name="additional-references-snippets-and-examples"></a>Дополнительные материалы, фрагменты кода и примеры

В этом примере показано, как вручную установить подключение к клиенту (требуется WMF5) для тестирования. 

```powershell
Update-DSCConfiguration –Wait -Verbose
```

Командлет [Add-DnsServerResourceRecordName](http://bit.ly/1G1H31L) используется для добавления записи CNAME типа в зону DNS. 

Функция PowerShell для [создания контрольной суммы и публикации MOF-файлов DSC на опрашивающем SMB-сервере](http://bit.ly/1E46BhI) автоматически создает необходимую контрольную сумму, а затем копирует MOF-файлы конфигурации и файлы контрольной суммы на опрашивающий SMB-сервер.

## <a name="appendix---understanding-odata-service-data-file-types"></a>Приложение. Основные сведения о типах файлов данных службы ODATA

Файл данных хранится для создания информации во время развертывания опрашивающего сервера, в состав которого входит веб-служба OData. Тип файла зависит от операционной системы, как описано ниже.

 - **Windows Server 2012**  
Файл всегда будет иметь тип MDB.
 - **Windows Server 2012 R2**  
Файл по умолчанию будет иметь тип EDB до тех пор, пока в конфигурации не будет указан тип MBD.

В [скрипте-примере расширенной конфигурации](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) по установке опрашивающего сервера также демонстрируется автоматическое управление параметрами файла web.config для предотвращения ошибок, вызванных типом файла.

