# Дополнительное значение для свойства RefreshMode

В этом выпуске появилось новое значение `RefreshMode` — **Disabled**. Когда включен этот режим, LCM не осуществляет управление документами. Этот режим можно применять, если вы работаете со средством конфигурации стороннего разработчика вместо DSC, но при этом все равно используете ресурсы DSC с помощью командлета `Invoke-DscResource`, либо когда нужно остановить обработку DSC по любой причине.

```powershell
Configuration LCMSettings
{
    Node localhost
    {
        LocalConfigurationManager
        {
           RefreshMode = 'Disabled'
        }
    }
}

LCMSettings -OutputPath .\LCMSettings
Set-DscLocalConfigurationManager -Path .\LCMSettings -Verbose -ComputerName localhost
```
<!--HONumber=Mar16_HO2-->
