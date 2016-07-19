# Частоты для RefreshMode и ConfigurationMode не должны быть кратными друг другу

В предыдущей версии DSC локальный диспетчер конфигураций рассматривал `RefreshFrequencyMins` и `ConfigurationModeFrequencyMins` как кратные друг другу. В WMF 5.0 RTM эти свойства обрабатываются независимо друг от друга. 

Дополнительные сведения см. в разделе [Настройка локального диспетчера конфигураций](https://msdn.microsoft.com/powershell/dsc/metaconfig).

<!--HONumber=Jul16_HO1-->


