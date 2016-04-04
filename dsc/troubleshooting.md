# Устранение неполадок в DSC

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

В этом разделе описываются методы устранения ошибок при запуске сценариев настройки требуемого состояния (DSC). Устранять ошибки DSC можно более эффективно, используя файлы журналов для отслеживания ошибок и понимая, как повторно использовать кэш для просмотра немедленных результатов изменения ресурсов. Эти методы обсуждаются в двух следующих разделах:

* Мой сценарий не запускается: **Диагностика ошибок в сценариях с помощью журналов DSC**
* Мои ресурсы не обновляются: **Как сбросить кэш**

## Мой сценарий не запускается: диагностика ошибок в сценариях с помощью журналов DSC

Как и все программное обеспечение Windows, DSC записывает ошибки и события в [журналы](https://msdn.microsoft.com/library/windows/desktop/aa363632.aspx) , которые можно просмотреть в [средстве просмотра событий](http://windows.microsoft.com/windows/what-information-event-logs-event-viewer). Анализ этих журналов может помочь в выявлении причины сбоя конкретной операции и избежать его в будущем. Написание сценариев настройки может быть непростой задачей. Чтобы упростить отслеживание ошибок, используйте ресурс журнала DSC, чтобы ход конфигурации отражался в аналитическом журнале событий DSC.

## Где находятся журналы событий DSC?

В средстве просмотра событий события DSC находятся в следующем разделе: **Журналы служб и приложений/Microsoft/Windows/Настройка требуемого состояния**.

Кроме того, для просмотра журналов событий можно запустить соответствующий командлет PowerShell [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx):

```
PS C:\> Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
   ProviderName: Microsoft-Windows-DSC
TimeCreated                     Id LevelDisplayName Message                                                                                                  
-----------                     -- ---------------- -------                                                                                                  
11/17/2014 10:27:23 PM        4102 Information      Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} : 
```

Как показано выше, основное имя журнала DSC — **Microsoft->Windows->DSC** (другие имена журналов в Windows для краткости здесь не показаны). Основное имя журнала добавляется к имени канала для получения полного имени журнала. DSC производит запись преимущественно в журналы трех типов: [операционные, аналитические и отладочные](https://technet.microsoft.com/library/cc722404.aspx). Так как аналитический и отладочный журналы по умолчанию отключены, их следует включить в средстве просмотра событий. Чтобы сделать это, откройте средство просмотра событий, введя "Show-EventLog" в Windows PowerShell или нажав кнопку **Пуск** и выбрав пункты **Панель управления**, **Администрирование** и **Средство просмотра событий**. В средстве просмотра событий в меню **Представление** выберите команду **Показать аналитический и отладочный журналы**. Имя журнала для аналитического канала — **Microsoft-Windows-Dsc/Analytic**, для отладочного канала — **Microsoft-Windows-Dsc/Debug**. Кроме того, для включения журналов можно воспользоваться средством [wevtutil](https://technet.microsoft.com/library/cc732848.aspx), как показано в следующем примере.

```powershell
wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
```

## Что содержат журналы DSC?

Журналы DSC разделяются на три канала в зависимости от важности сообщения. Операционный журнал в DSC содержит все сообщения об ошибках и может использоваться для выявления проблем. Аналитический журнал содержит больше событий, и с его помощью можно определить, где произошли ошибки. Кроме того, этот канал содержит подробные сообщения (если они имеются). Отладочный журнал помогает понять, как произошли ошибки. Сообщения о событиях DSC структурированы таким образом, что каждое сообщение о событии начинается с идентификатора задания, который уникальным образом представляет операцию DSC. В приведенном ниже примере предпринимается попытка получить сообщение из первого события, записанного в операционный журнал DSC.

```powershell
PS C:\> $AllDscOpEvents = Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
PS C:\> $FirstOperationalEvent = $AllDscOpEvents[0]
PS C:\> $FirstOperationalEvent.Message
Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} : 
Consistency engine was run successfully. 
```

События DSC записываются в определенной структуре, что позволяет пользователю собрать все события из одного задания DSC. Эта структура выглядит следующим образом:

**Идентификатор задания: <Guid>**
**<Event Message>**

## Сбор событий для отдельной операции DSC

Журналы событий DSC содержат события, созданные при выполнении различных операций DSC. Однако обычно вас интересуют сведения только для одной конкретной операции. Все журналы DSC можно группировать по свойству ID задания, которое является уникальным для каждой операции DSC. Идентификатор задания отображается в виде первого значения свойства во всех событиях DSC. Далее описывается процесс сбора всех событий в структуре сгруппированного массива.

```powershell
<##########################################################################
 Step 1 : Enable analytic and debug DSC channels (Operational channel is enabled by default)
###########################################################################>
 
wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
wevtutil.exe set-log “Microsoft-Windows-Dsc/Debug” /q:True /e:true
 
<##########################################################################
 Step 2 : Perform the required DSC operation (Below is an example, you could run any DSC operation instead)
###########################################################################>
 
Get-DscLocalConfigurationManager
 
<##########################################################################
Step 3 : Collect all DSC Logs, from the Analytic, Debug and Operational channels
###########################################################################>
 
$DscEvents=[System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Operational") `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Analytic" -Oldest) `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Debug" -Oldest)
 
 
<##########################################################################
 Step 4 : Group all logs based on the job ID
###########################################################################>
$SeparateDscOperations = $DscEvents | Group {$_.Properties[0].value}  
```

Здесь переменная `$SeparateDscOperations` содержит журналы, сгруппированные по идентификаторам заданий. Каждый элемент массива этой переменной представляет группу событий, записанных различными операциями DSC, что позволяет получить дополнительные сведения о журналах.

```
PS C:\> $SeparateDscOperations
 
Count Name                      Group                                                                     
----- ----                      -----                                                                     
   48 {1A776B6A-5BAC-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
   40 {E557E999-5BA8-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
PS C:\> $SeparateDscOperations[0].Group
   ProviderName: Microsoft-Windows-DSC
TimeCreated                     Id LevelDisplayName Message                                               
-----------                     -- ---------------- -------                                               
12/2/2013 3:47:29 PM          4115 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4198 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4114 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4102 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4176 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...       
```

С помощью [Where-Object](https://technet.microsoft.com/library/ee177028.aspx) можно извлечь данные в переменную `$SeparateDscOperations`. Ниже приведены пять ситуаций, в которых может потребоваться извлечь данные для устранения неполадок DSC:

### 1. Сбой при выполнении операции

Все события имеют [уровни серьезности](https://msdn.microsoft.com/library/dd996917(v=vs.85)). С помощью этих сведений можно определить события с ошибкой:

```
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.LevelDisplayName -contains "Error"}
Count Name                      Group                                                                     
----- ----                      -----                                                                     
   38 {5BCA8BE7-5BB6-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
```

### 2. Подробные сведения об операциях за последние полчаса

`TimeCreated`, свойство каждого события Windows, содержит время создания события. Для фильтрации событий можно сравнить это свойство с конкретным объектом даты и времени:

```powershell
PS C:\> $DateLatest = (Get-Date).AddMinutes(-30)
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.TimeCreated -gt $DateLatest}
Count Name                      Group                                                                     
----- ----                      -----                                                                     
    1 {6CEC5B09-5BB0-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord}   
```

### 3. Сообщения последней операции

Последняя операция хранится по первому индексу в группе массива `$SeparateDscOperations`. При запросе сообщений группы для индекса 0 возвращаются всех сообщения для последней операции:

```powershelll
PS C:\> $SeparateDscOperations[0].Group.Message
Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} : 
Running consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : 
Configuration is sent from computer NULL by user sid S-1-5-18.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : 
Displaying messages from built-in DSC resources:
 WMI channel 1 
 ResourceID:  
 Message : [INCH-VM]:                            [] Starting consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : 
Displaying messages from built-in DSC resources:
 WMI channel 1 
 ResourceID:  
 Message : [INCH-VM]:                            [] Consistency check completed. 
```

### 4. Сообщения об ошибках в журнале для последних неудачных операций

`$SeparateDscOperations[0].Group` содержит набор событий для последней операции. Запустите командлет `Where-Object` для фильтрации событий в зависимости от их отображаемого уровня. Результаты сохраняются в переменной `$myFailedEvent`, которую можно разделить на составные части для получения сообщения о событии:

```powershell
PS C:\> $myFailedEvent = ($SeparateDscOperations[0].Group | Where-Object {$_.LevelDisplayName -eq "Error"})
 
PS C:\> $myFailedEvent.Message
Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} : 
DSC Engine Error : 
 Error Message Current configuration does not exist. Execute Start-DscConfiguration command with -Path pa
rameter to specify a configuration file and create a current configuration first. 
Error Code : 1 
```

### 5. Все события, созданные для идентификатора конкретного задания

`$SeparateDscOperations` представляет собой массив групп, каждая из которых имеет имя, являющееся уникальным идентификатором задания. Запустив командлет `Where-Object`, можно извлечь группы событий, которые имеют идентификатор конкретного задания:

```powershell
PS C:\> ($SeparateDscOperations | Where-Object {$_.Name -eq $jobX} ).Group

   ProviderName: Microsoft-Windows-DSC
 
TimeCreated                     Id LevelDisplayName Message                                               
-----------                     -- ---------------- -------                                               
12/2/2013 4:33:24 PM          4102 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...      
12/2/2013 4:33:24 PM          4168 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...      
12/2/2013 4:33:24 PM          4146 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...      
12/2/2013 4:33:24 PM          4120 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...  
```

## Анализ журналов DSC с помощью xDscDiagnostics

**xDscDiagnostics** представляет собой модуль PowerShell, состоящий из двух простых функций, которые могут помочь в анализе сбоев DSC на вашем компьютере: это `Get-xDscOperation` и `Trace-xDscOperation`. Эти функции помогают идентифицировать все локальные события для последних операций DSC или событий DSC на удаленных компьютерах (с действительными учетными данными). В данном случае термин "операция DSC" используется для определения одного уникального выполнения DSC от начала до конца. Например, `Test-DscConfiguration` будет отдельной операцией DSC. Аналогично все остальные командлеты в DSC (такие как `Get-DscConfiguration`, `Start-DscConfiguration` и т. д.) можно определить как отдельные операции DSC. Пояснения к этим двум функциям приведены в модуле PowerShell [xDscDiagnostics](https://powershellgallery.com/packages/xDscDiagnostics) (набор ресурсов DSC). Более подробные объяснения даны ниже. Чтобы получить справку, выполните команду `Get-Help <cmdlet name>`.

## Get-xDscOperation

Эта функция позволяет найти результаты операций DSC, выполняемых на одном или нескольких компьютерах, и возвращает объект, содержащий коллекцию событий, созданных при выполнении каждой операции DSC. Например, в следующем выводе были запущены три команды. Первая была выполнена успешно, две остальные — неудачно. Эти результаты сводятся в выводе `Get-xDscOperation`.

TODO: заменить этот рисунок на вывод Get-xDscOperation

### Параметры

* **Newest**: принимает целое число для указания количества отображаемых операций. По умолчанию возвращается 10 последних операций. Например,
  TODO: Show Get-xDscOperation -Newest 5
* **ComputerName**: параметр, который принимает массив строк. Каждая из этих строк содержит имя компьютера, с которого необходимо собрать данные журналов событий DSC. По умолчанию данные собираются с локального компьютера. Чтобы включить эту возможность, необходимо выполнить следующую команду на удаленных компьютерах в режиме с повышенными правами, который разрешает сбор событий
```powershell
  New-NetFirewallRule -Name "Service RemoteAdmin" -Action Allow
```
* **Credential**: параметр типа PSCredential, который помогает получить доступ к компьютерам, указанным в параметре ComputerName.

### Возвращаемый объект

Командлет возвращает массив объектов типа **Microsoft.PowerShell.xDscDiagnostics.GroupedEvents**. Каждый объект в этом массиве относится к отдельной операции DSC. Отображение по умолчанию для этого объекта имеет следующие свойства.
* **SequenceID**: задает добавочный номер, присваиваемый операции DSC на основе времени ее выполнения. Например, последняя выполняемая операция будет иметь SequenceID, равный 1, предпоследняя — 2 и т. д. Это число является еще одним идентификатором для каждого объекта в возвращаемом массиве.
* **TimeCreated**: значение типа DateTime, указывающее время начала операции DSC.
* **ComputerName**: имя компьютера, результаты для которого объединяются.
* **Result**: строка со значением **Failure** или **Success**, указывающая, возникла ошибка при выполнении этой операции DSC или нет.
* **AllEvents**: объект, представляющий коллекцию всех событий, созданных операцией DSC.

Например, в выходных данных ниже показаны результаты выполнения последней операции с нескольких компьютеров:
  TODO: заменить рисунок для Get-xDscOperation на журналы отображения для удаленного компьютера

## Trace-xDscOperation

Этот командлет возвращает объект, содержащий коллекцию событий, их типы и выводимые сообщения, созданные при выполнении определенной операции DSC. Как правило, при обнаружении сбоя в любых операциях с помощью `Get-xDscOperation` необходимо выполнить трассировку этой операции, чтобы узнать, какое из событий вызвало сбой.

### Параметры

* **SequenceID**: это целочисленное значение, назначаемое любой операции и относящееся к конкретному компьютеру. Так, если указать SequenceID равным 4, то будет выведена трассировка четвертой по счету операции DSC, начиная с последней.

Trace-xDscOperation с указанным идентификатором последовательности
* **JobID**: это значение типа GUID, назначаемое локальным диспетчером конфигураций операции xDscOperation для уникальной идентификации операции. Если JobID указан, выводится трассировка соответствующей операции DSC.
  TODO: заменить рисунок для Trace-xDscOperation, принимающей JobID в качестве параметра
* **ComputerName** и **Credential**: эти параметры позволяют собирать трассировку с удаленных компьютеров:
```powershell
New-NetFirewallRule -Name "Service RemoteAdmin" -Action Allow
```
  TODO: заменить рисунок для операции Trace-xDscOperation, выполняемой на другом компьютере

Обратите внимание, что поскольку `Trace-xDscOperation` объединяет события из аналитических, отладочных и операционных журналов, вам будет предложено включить эти журналы, как описано выше.

### Возвращаемый объект

Командлет возвращает массив объектов типа `Microsoft.PowerShell.xDscDiagnostics.TraceOutput`. Каждый объект в этом массиве содержит следующие поля:
* **ComputerName**: имя компьютера, с которого собираются журналы.
* **EventType**: это поле типа перечислителя, содержащее сведения о типе события. Оно может принимать одно из следующих значений:
  - *Operational* — это событие из операционного журнала.
  - *Analytic* — это событие из аналитического журнала.
  - *Debug* — это событие из отладочного журнала.
  - *Verbose* — события выводятся в виде подробных сообщений во время выполнения. Эти подробные сообщения позволяют легко определить последовательность публикуемых событий.
  - *Error* — события для ошибок. Ища события для ошибок, можно быстро найти причину проблемы.
* **TimeCreated** — значение типа DateTime, указывающее время регистрации события в DSC.
* **Message** — сообщение, которое было записано DSC в журналы событий.

Ниже перечислены поля этого объекта, с помощью которых можно получить дополнительные сведения о событии, но которые не отображаются по умолчанию:

* **JobID** — идентификатор задания (в формате GUID) для этой операции DSC.
* **SequenceID** — SequenceID, уникальный для этой операции DSC на этом компьютере.
* **Event** — фактическое событие, записанное DSC. Оно имеет тип `System.Diagnostics.Eventing.Reader.EventLogRecord`. Кроме того, его можно получить, запустив командлет `Get-WinEvent`. Оно содержит дополнительные сведения, такие как задача, идентификатор события и уровень события.

Кроме того, можно собирать информацию о событиях, сохраняя результат в переменную `Trace-xDscOperation`. Чтобы отобразить все события для определенной операции DSC, можно использовать следующую команду:

```powershell
(Trace-xDscOperation -SequenceID 3).Event
```

Она отобразит те же результаты, что и командлет `Get-WinEvent`, как показано в выходных данных ниже:
  TODO: какие выходные данные?

В идеальном случае сначала нужно получить список последних конфигураций DSC, запущенных на ваших компьютерах, с помощью `Get-xDscOperation`. После этого можно исследовать отдельные операции (на основе идентификаторов SequenceID или JobID) при помощи команды `Trace-xDscOperation`, чтобы узнать, что именно сделала эта операция.

## Мои ресурсы не обновляются: как сбросить кэш

Для повышения эффективности подсистема DSC кэширует ресурсы, которые реализованы в виде модулей PowerShell. Однако это может вызвать проблемы при одновременной разработке и тестировании ресурса, так как DSC будет загружать кэшированную версию до тех пор, пока процесс не будет перезапущен. Единственный способ принудительной загрузки новой версии в DSC — явным образом завершить процесс подсистемы DSC.

Аналогично при запуске `Start-DscConfiguration` после добавления и изменения пользовательских ресурсов эти изменения могут вступить в силу только после перезагрузки компьютера. Это вызвано тем, что DSC выполняется в хост-процессе поставщика WMI (WmiPrvSE). Обычно существует несколько экземпляров WmiPrvSE, которые выполняются одновременно. После перезагрузки хост-процесс перезапускается и кэш очищается.

Для успешного обновления конфигурации и очистки кэша без перезагрузки необходимо остановить и перезапустить хост-процесс. Это можно сделать отдельно для каждого экземпляра, определив процесс, остановив и перезапустив его. Кроме того, вы можете использовать `DebugMode` для перезагрузки ресурсов PowerShell DSC, как показано ниже.

Для определения процесса, в котором размещается подсистема DSC, и остановки этого процесса для каждого экземпляра сначала получите идентификатор процесса WmiPrvSE, в котором размещена подсистема DSC. Затем для обновления поставщика остановите процесс WmiPrvSE, используя приведенную ниже команду, а затем еще раз запустите командлет **Start-DscConfiguration**.

```powershell
###
### find the process that is hosting the DSC engine
###
$dscProcessID = Get-WmiObject msft_providers | 
Where-Object {$_.provider -like 'dsccore'} | 
Select-Object -ExpandProperty HostProcessIdentifier 

###
### Stop the process
###
Get-Process -Id $dscProcessID | Stop-Process
```

## Использование DebugMode

Можно настроить локальный диспетчер конфигурации DSC, так чтобы он всегда очищал кэш с помощью `DebugMode` при перезапуске хост-процесса. При установке значения **TRUE** ядро всегда перегружает ресурс PowerShell DSC. После завершения записи ресурса можно снова установить свойство равным **FALSE**, и подсистема вернется к кэшированию модулей.

Ниже приведена демонстрация автоматического обновления кэша с помощью `DebugMode`. Во-первых, давайте взглянем на конфигурацию по умолчанию:

```
PS C:\> Get-DscLocalConfigurationManager
 
 
AllowModuleOverwrite           : False
CertificateID                  : 
ConfigurationID                : 
ConfigurationMode              : ApplyAndMonitor
ConfigurationModeFrequencyMins : 30
Credential                     : 
DebugMode                      : False
DownloadManagerCustomData      : 
DownloadManagerName            : 
LocalConfigurationManagerState : Ready
RebootNodeIfNeeded             : False
RefreshFrequencyMins           : 15
RefreshMode                    : PUSH
PSComputerName                 :  
```

Вы видите, что значение `DebugMode` установлено равным **FALSE**.

Чтобы настроить демонстрацию `DebugMode`, используйте следующий ресурс PowerShell:

```powershell
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    "1" | Out-File -PSPath "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return $false
} 
```

Теперь создайте конфигурацию с именем `TestProviderDebugMode` с помощью этого ресурса:

```powershell
Configuration ConfigTestDebugMode
{
    Import-DscResource -Name TestProviderDebugMode
    Node localhost
    {
        TestProviderDebugMode test
        {
            onlyProperty = "blah"
        }
    }
}
ConfigTestDebugMode
```

Вы увидите, что файл: **$env:SystemDrive\OutputFromTestProviderDebugMode.txt** содержит **1**.

Теперь обновите код поставщика с помощью следующего сценария:

```powershell
$newResourceOutput = Get-Random -Minimum 5 -Maximum 30
$content = @"
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    "$newResourceOutput" | Out-File -PSPath C:\OutputFromTestProviderDebugMode.txt
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return `$false
}
"@ | Out-File -FilePath "C:\Program Files\WindowsPowerShell\Modules\MyPowerShellModules\DSCResources\TestProviderDebugMode\TestProviderDebugMode.psm1
```

Этот сценарий создает случайное число и соответствующим образом обновляет код поставщика. Если `DebugMode` установлено равным false, содержимое файла **$env:SystemDrive\OutputFromTestProviderDebugMode.txt** не изменяется.

Теперь установите `DebugMode` равным **TRUE** в сценарии настройки:

```powershell
LocalConfigurationManager
{
    DebugMode = $true
} 
```

При запуске приведенного выше сценария вы увидите, что содержимое файла каждый раз будет другим. (Проверить это можно с помощью `Get-DscConfiguration`.) Ниже приведен результат двух дополнительных запусков (у вас могут получиться другие результаты).

```powershell
PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)
 
onlyProperty                            PSComputerName                         
------------                            --------------                         
20                                      localhost                              
 
PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)
 
onlyProperty                            PSComputerName                         
------------                            --------------                         
14                                      localhost
```

## См. также

### Ссылка
* [Ресурс Log в DSC](logResource.md)

### Концепции
* [Создание пользовательских ресурсов настройки требуемого состояния Windows PowerShell](authoringResource.md)

### Прочие ресурсы
* [Командлеты настройки требуемого состояния PowerShell](https://technet.microsoft.com/en-us/library/dn521624(v=wps.630).aspx)


<!--HONumber=Mar16_HO1-->


