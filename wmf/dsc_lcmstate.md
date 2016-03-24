# Подробные сведения о состоянии LCM

Мы внесли улучшения процесс предоставления сведений о состоянии LCM. LCMState, возвращаемый Get-DscLocalConfigurationManager, теперь может содержать следующие значения:

* **Idle**
* **Занято**
* **PendingReboot**
* **PendingConfiguration**

Мы также добавили свойство LCMStateDetail, содержащее дополнительные сведения о состоянии.
<!--HONumber=Mar16_HO2-->
