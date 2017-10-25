---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: f3c218fc668e35fa50047459d8031d77cdf985a2
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="reporting-on-jea"></a>Отчеты о JEA
Чтобы отправить отчета о состоянии конфигурации JEA, можно использовать следующее.
1.  **Get-PSSessionConfiguration** для получения списка всех зарегистрированных конечных точек на заданном компьютере.
2.  **Get-PSSessionCapability** для получения отчета о возможности любого пользователя на заданной конечной точке.

Ниже приведен пример использования **Get-PSSessionCapability**:
```powershell
Get-PSSessionCapability -ConfigurationName Maintenance -Username "CONTOSO\JohnDoe"

CommandType     Name                                               Version    Source           
-----------     ----                                               -------    ------           
Alias           clear -> Clear-Host                                                            
Alias           cls -> Clear-Host                                                              
Alias           exsn -> Exit-PSSession                                                         
Alias           gcm -> Get-Command                                                             
Alias           measure -> Measure-Object                                                      
Alias           select -> Select-Object                                                        
Function        Clear-Host                                                                     
Function        Exit-PSSession                                                                 
Function        Get-Command                                                                    
Function        Get-FormatData                                                                 
Function        Get-Help                                                                       
Function        Get-UserInfo                                                                   
Function        Measure-Object                                                                 
Function        Out-Default                                                                    
Function        Select-Object                                                                  
Cmdlet          Restart-Service                                    3.0.0.0 Microsof...


```

Чтобы отправить отчет о _действиях_, выполненных пользователем во время сеанса JEA, можно выполнить следующее:
1. Включить записи с запросом на повышение прав для этой конечной точки JEA и обратиться к каталогу записей получения полного журнала действий каждого пользователя.
2. Включить ведение журнала модуля PowerShell и просмотреть журналы событий PowerShell.

