# Единое и согласованное представление состояний

В этот выпуск внесен ряд усовершенствований для служб автоматизации, отвечающих за состояние LCM и DSC. Сюда входят единые и согласованные представления состояния, управляемое свойство datetime объектов состояния, возвращаемых командлетом Get-DscConfigurationStatus, и свойство расширенных сведений о состоянии LCM, возвращаемое командлетом Get-DscLocalConfigurationManager.

Это представление состояния LCM и DSC пересмотрено и унифицировано согласно следующим правилам:
1.  Необработанный ресурс не влияет на состояние LCM и DSC.
2.  LCM останавливает обработку дальнейших ресурсов, встретив ресурс, который требует перезагрузку.
3.  Ресурс, требующий перезагрузку, не находится в нужном состоянии до ее фактического выполнения.
4.  После обнаружения ресурса, завершающегося сбоем, LCM продолжает обрабатывать дальнейшие ресурсы, если только они не зависят от ресурса со сбоем.
5.  Общее состояние, возвращаемое командлетом Get-DscConfigurationStatus, представляет собой супермножество состояния для всех ресурсов.
6.  Состояние PendingReboot является супермножеством состояния PendingConfiguration.

В следующей таблице приведены итоговые свойства состояния в несколько типичных сценариях:

| **Сценарий**                    | **LCMState\***       | **Состояние** | **Запрошена перезагрузка**  | **ResourcesInDesiredState**  | **ResourcesNotInDesiredState** |
|---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
| S**^**                          | Idle                 | Успех    | $false        | S                            | $null                          |
| F**^**                          | PendingConfiguration | Отказ    | $false        | $null                        | F                              |
| S,F                             | PendingConfiguration | Отказ    | $false        | S                            | F                              |
| F,S                             | PendingConfiguration | Отказ    | $false        | S                            | F                              |
| S<sub>1</sub>, F, S<sub>2</sub> | PendingConfiguration | Отказ    | $false        | S<sub>1</sub>, S<sub>2</sub> | F                              |
| F<sub>1</sub>, S, F<sub>2</sub> | PendingConfiguration | Отказ    | $false        | S                            | F<sub>1</sub>, F<sub>2</sub>   |
| S, r                            | PendingReboot        | Успех    | $true         | S                            | r                              |
| F, r                            | PendingReboot        | Отказ    | $true         | $null                        | F, r                           |
| r, S                            | PendingReboot        | Успех    | $true         | $null                        | r                              |
| r, F                            | PendingReboot        | Успех    | $true         | $null                        | r                              |

^
S<sub>i</sub>: ряд ресурсов, которые успешно применены.
F<sub>i</sub>: ряд ресурсов, которые применены с ошибкой.
r: ресурс, который требует перезагрузку.
\*

```powershell
$LCMState = (Get-DscLocalConfigurationManager).LCMState
$Status = (Get-DscConfigurationStatus).Status

$RebootRequested = (Get-DscConfigurationStatus).RebootRequested

$ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

$ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
```
## Улучшения в командлете Get-DscConfigurationStatus

В этом выпуске в командлет Get-DscConfigurationStatus было внесено несколько улучшений. Ранее свойство StartDate объектов, возвращаемое командлетом StartDate, имело тип String. Теперь оно имеет тип Datetime, что упрощает сложный выбор и фильтрацию благодаря встроенным свойствам объекта Datetime.
```powershell
(Get-DscConfigurationStatus).StartDate | fl \*
DateTime : Friday, November 13, 2015 1:39:44 PM
Date : 11/13/2015 12:00:00 AM
Day : 13
DayOfWeek : Friday
DayOfYear : 317
Hour : 13
Kind : Local
Millisecond : 886
Minute : 39
Month : 11
Second : 44
Ticks : 635830187848860000
TimeOfDay : 13:39:44.8860000
Year : 2015
```

Ниже приведен пример, который возвращает все записи операций DSC, созданные в тот же день недели, что и сегодня.
```powershell
(Get-DscConfigurationStatus –All) | where { $\_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

Записи операций, которые не вносят изменения в конфигурацию узла (т. е. представлены операциями только для чтения), исключаются. Таким образом, операции Test-DscConfiguration и Get-DscConfiguration больше не имитируются в возвращаемых объектах из командлета Get-DscConfigurationStatus.
В выходные данные командлета Get-DscConfigurationStatus добавляются записи для операции настройки метаконфигурации.

Ниже приведен пример результата, возвращаемого из командлета DscConfigurationStatus –All.
```powershell
All configuration operations:

Status StartDate Type RebootRequested
------ --------- ---- ---------------
Success 11/13/2015 11:38:16 AM Consistency False
Success 11/13/2015 11:23:16 AM Reboot False
Success 11/13/2015 11:21:43 AM Reboot True
Success 11/13/2015 11:20:44 AM Initial True
Success 11/13/2015 11:20:44 AM LocalConfigurationManager False
```

## Улучшения в командлете Get-DscLocalConfigurationManager
В объект, возвращаемый из командлета Get-DscLocalConfigurationManager, добавлено новое поле LCMStateDetail. Оно заполняется в том случае, когда LCMState имеет значение Busy. Извлечь его можно с помощью следующего командлета:
```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

Ниже приведен пример выходных данных для постоянного мониторинга конфигурации, которая требует двух перезагрузок на удаленном узле.
```powershell
Start a configuration that requires two reboots

Monitor LCM State:
LCM State: Busy, LCM is applying a new configuration.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: Idle,
LCM State: Busy, LCM is performing a consistency check.
LCM State: Idle,
```
<!--HONumber=Mar16_HO2-->
