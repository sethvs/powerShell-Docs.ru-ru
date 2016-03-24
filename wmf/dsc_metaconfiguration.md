# Настройка LCM DSC с помощью нового атрибута метаконфигурации

Атрибут `DscLocalConfigurationManager` определяет блок конфигурации как метаконфигурацию, которая используется для настройки локального диспетчера конфигураций (LCM) DSC. Этот атрибут ограничивает конфигурацию, допуская только элементы для настройки локального диспетчера конфигураций DSC. Во время обработки эта конфигурация создает файл `*.meta.mof`, который затем отправляется на соответствующие целевые узлы с помощью командлета `Set-DscLocalConfigurationManager`.

```powershell
[DscLocalConfigurationManager()]
configuration meta
{
    Node localhost
    {
        Settings
        {
            ConfigurationMode = "ApplyAndAutocorrect"
            ConfigurationID = "5603f952-d6c6-4971-88c4-948636bf5c3f"
            RefreshMode = "Pull"
        }
        ConfigurationRepositoryWeb PullServer
        {
            ServerURL = "https://corp.contoso.com/PSDSCPullServer/PSDSCPullServer.svc"
        }
    }
}
```

Приведенный выше пример настраивает для LCM режим обновления с извлечением, изменяет режим конфигурации на ApplyAndAutocorrect, а также определяет тип и расположение опрашивающего сервера.

Этот новый атрибут конфигурации заменяет и расширяет функциональность ресурса LocalConfigurationManager из PowerShell 4.0. LocalConfigurationManager по-прежнему допускается в конфигурациях без этого атрибута для обеспечения обратной совместимости.

Метаресурсы:

| **Имя ресурса**            | **Описание**                                |
|------------------------------|------------------------------------------------|
| LocalConfigurationManager    | Различные параметры для выполнения подсистемы DSC      |
| PartialConfiguration         | Параметры неполной конфигурации                 |
| ConfigurationRepositoryWeb   | Репозиторий конфигураций в Интернете             |
| ConfigurationRepositoryShare | Репозиторий конфигураций на основе общей папки      |
| ResourceRepositoryWeb        | Репозиторий конфигураций в Интернете                  |
| ResourceRepositoryShare      | Репозиторий ресурсов на основе файлов                 |
| ReportServerWeb              | Конечная точка отчетов в Интернете для сценария извлечения |
<!--HONumber=Mar16_HO2-->
