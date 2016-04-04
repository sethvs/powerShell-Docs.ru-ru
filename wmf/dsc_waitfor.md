# Указание межузловых зависимостей

Встроенные ресурсы WaitFor\* (WaitForAll, WaitForAny и WaitForSome) позволяют указать зависимости между компьютерами во время выполнения конфигурации без внешней оркестрации. Поведение каждого ресурса WaitFor\* имеет следующий вид:

* <ctype="x-NOTFOUND" mdpre="**" mdpost="**">WaitForAll</ctype="x-NOTFOUND">: ожидает, пока указанный ресурс не примет нужное состояние на <ctype="x-NOTFOUND" mdpre="*" mdpost="*">всех</ctype="x-NOTFOUND"> целевых узлах, определенных в свойстве NodeName.
* <ctype="x-NOTFOUND" mdpre="**" mdpost="**">WaitForAny</ctype="x-NOTFOUND">: ожидает, пока указанный ресурс не примет нужное состояние на <ctype="x-NOTFOUND" mdpre="*" mdpost="*">любом</ctype="x-NOTFOUND"> целевом узле, определенном в свойстве NodeName.
* <ctype="x-NOTFOUND" mdpre="**" mdpost="**">WaitForSome</ctype="x-NOTFOUND">: ожидает, пока указанный ресурс не примет нужное состояние на таком числе определенных в свойстве NodeName целевых узлов, которое задано в свойстве NodeCount.

Эти ресурсы обеспечивают синхронизацию между узлами с помощью CIM-подключений по протоколу WS-Man. С их помощью конфигурация может ожидать изменения состояния определенного ресурса на другом компьютере, прежде чем продолжить собственное выполнение. 

Например, в следующей конфигурации целевой узел ожидает выполнения ресурса <ctype="x-NOTFOUND" mdpre="**" mdpost="**">xADDomain</ctype="x-NOTFOUND"> на узле <ctype="x-NOTFOUND" mdpre="**" mdpost="**">MyDC</ctype="x-NOTFOUND"> с несколькими повторными попытками, прежде чем присоединиться к домену.

```PowerShell
Configuration JoinDomain

{
    Import-DscResource -Module xComputerManagement

    WaitForAll DC
    {
        ResourceName      = '[xADDomain]NewDomain'
        NodeName          = 'MyDC'
        RetryIntervalSec  = 15
        RetryCount        = 30
    }

    xComputer JoinDomain
    {
        Name             = 'MyPC'
        DomainName       = 'Contoso.com'
        Credential       = (get-credential)
        DependsOn        ='[WaitForAll]DC'
    }
}
```
<ctype="x-NOTFOUND" mdpre="**" mdpost="**">Совет</ctype="x-NOTFOUND">. По умолчанию ресурсы WaitFor\* выполняют одну попытку и далее завершаются со сбоем. Поэтому, хотя это и необязательно, обычно стоит указать интервал и число повторов.


<!--HONumber=Mar16_HO3-->


