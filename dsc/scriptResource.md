# Ресурс Script в DSC

 
> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс **Script** в DSC Windows PowerShell предоставляет механизм запуска блоков сценариев на целевых узлах.

## Синтаксис

```
Script [string] #ResourceName
{
    GetScript = [string]
    SetScript = [string]
    TestScript = [string]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## Свойства

|  Свойство  |  Описание   | 
|---|---| 
| GetScript| Предоставляет блок сценария Windows PowerShell, который выполняется при вызове командлета [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx). Этот блок должен возвращать хэш-таблицу.| 
| SetScript| Предоставляет блок сценария Windows PowerShell. При вызове командлета[Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) в первую очередь выполняется блок **TestScript**. Если блок **TestScript** возвращает **$false**, будет запущен блок **SetScript**. Если блок **TestScript** возвращает **$true**, то блок **SetScript** запущен не будет.| 
| TestScript| Предоставляет блок сценария Windows PowerShell. Этот блок запускается при вызове командлета[Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx). Если он возвращает **$false**, будет запущен блок SetScript. Если он возвращает **$true**, блок SetScript запущен не будет. Кроме того, блок **TestScript** запускается при вызове командлета [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx). Однако в этом случае блок **SetScript** не будет запущен независимо от того, какое значение возвращает блок TestScript. Блок **TestScript** должен вернуть True, если фактическая конфигурация соответствует текущей конфигурации требуемого состояния, и False в противном случае. (Текущей конфигурацией требуемого состояния является последняя конфигурация, активированная на узле, который использует DSC.)| 
| Учетные данные| Указывает учетные данные, используемые для запуска этого сценария, если они необходимы.| 
| DependsOn| Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.

## Пример
```powershell
Script ScriptExample
{
    SetScript = { 
        $sw = New-Object System.IO.StreamWriter("C:\TempFolder\TestFile.txt")
        $sw.WriteLine("Some sample string")
        $sw.Close()
    }
    TestScript = { Test-Path "C:\TempFolder\TestFile.txt" }
    GetScript = { <# This must return a hash table #> }          
}
```

<!--HONumber=Feb16_HO4-->
