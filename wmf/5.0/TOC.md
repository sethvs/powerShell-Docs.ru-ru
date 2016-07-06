# [Обзор заметок о выпуске WMF](releasenotes.md)

# [Сведения об установке](requirements.md)

# [Состояние совместимости продуктов](productincompat.md)

# [Отзывы](feedback.md)

# [Сценарии, поддерживаемые WMF 5.0]()
## [Just Enough Administration (JEA)](jea_overview.md)
### [Создание конечной точки JEA и подключение к ней](jea_endpoint.md)
### [Отчеты о JEA](jea_report.md)

## [Создание настраиваемых типов с помощью классов PowerShell](class_overview.md)
### [Определение настраиваемых типов](class_newtype.md)
### [Объявление базового класса](class_base.md)
### [Объявление реализованного интерфейса](class_interface.md)
### [Вызов конструктора базовых классов](class_baseconstructor.md)
### [Вызов метода базового класса](class_basemethod.md)

## [Усовершенствования отладки сценариев PowerShell](debug_overview.md)

## [Усовершенствования в настройке требуемого состояния (DSC)](dsc_improvements.md)
### [Конфигурации]()
#### [Указание межузловых зависимостей](dsc_waitfor.md)
#### [Зашифрованные MOF](dsc_encryptedmof.md)
#### [Поддержка справки для конфигурации DSC](dsc_confighelp.md)
#### [Усовершенствования создания с помощью интегрированной среды сценариев PowerShell](dsc_authoring.md)
#### [Поддержка идентичных повторяющихся ресурсов в конфигурации](dsc_identicalduplicate.md)
#### [Ключевое слово Import-DscResource поддерживает параметр -moduleversion](dsc_importdscresource.md)
#### [Поддержка ключевого слова Configuration в WOW64](dsc_wow64.md)
### [Ресурсы]()
#### [Ресурсы DSC, основанные на классах](dsc_classbasedresource.md)
#### [Отладка сценариев для ресурсов DSC](dsc_resourcedebugging.md)
#### [Поддержка автоматического запуска от имени для ресурсов DSC](dsc_runas.md)
#### [Поддержка параллельного управления версиями для ресурсов DSC](dsc_sxsresource.md)
#### [Новые ресурсы, входящие в комплект поставки](dsc_newresources.md)
### [Локальный диспетчер конфигураций]()
#### [Настройка узла с помощью нескольких фрагментов конфигурации](dsc_partialconfig.md)
##### [Поддержка смешанного режима RefreshMode](dsc_partialconfig_mixedmode.md)
#### [Настройка подсистемы DSC с помощью нового атрибута](dsc_metaconfiguration.md)
#### [Подробные сведения о состоянии LCM](dsc_lcmstate.md)
#### [Частоты для RefreshMode и ConfigurationMode не должны быть кратными друг другу](dsc_freqnomultiple.md)
#### [Дополнительное значение для свойства RefreshMode](dsc_refreshmode.md)
### [Командлеты]()
#### [Сведения о состоянии конфигурации](dsc_getconfigurationstatus.md)
#### [Командлет Test-DscConfiguration поддерживает проектные конфигурации](dsc_testconfiguration.md)
#### [Прямой доступ к методам ресурсов DSC](dsc_directaccess.md)
#### [Доставка документа конфигурации без применения](dsc_publishconfig.md)
#### [Удаление документов DSC](dsc_removeconfigdoc.md)
#### [Единое и согласованное представление состояний](dsc_statestatus.md)
#### [Командлет Set-DscLocalConfigurationManager поддерживает параметр -force](dsc_setdsclcm.md)
### [Режим Pull]()
#### [Извлечение по запросу для конфигураций DSC](dsc_updateconfig.md)
#### [Разделение идентификаторов узла и конфигурации](dsc_nodeid.md)
#### [Разделение репозиториев конфигураций, ресурсов и отчетов](dsc_repository.md)
#### [Отправка отчета о состоянии конфигурации в центральное расположение](dsc_reporting.md)

## [Аудит использования PowerShell с помощью записи и ведения журнала](audit_overview.md)
### [Расширенные параметры транскрибирования](audit_transcript.md)
### [Трассировка сценариев и ведения журналов для них](audit_script.md)
### [Командлеты Cryptographic Message Syntax (CMS)](audit_cms.md)

## [Обнаружение, установка и инвентаризация программного обеспечения с помощью PackageManagement](oneget_overview.md)
### [Командлеты PackageManagement](oneget_cmdlets.md)

## [Обнаружение, установка и инвентаризация модуля PowerShell с помощью PowerShellGet](psget_module_overview.md)
### [Регистрация репозитория PowerShell](psget_psrepository.md)
### [Поддержка параллельных версий в PowerShell 5.0 или более поздней версии](psget_modulesxsinstall.md)
### [Установка зависимостей модулей](psget_moduledependency.md)
### [Командлеты PowerShellGet для управления модулями](psget_modulecmdlets.md)

## [Установка компонента обнаружения сценариев PowerShell и управление им с помощью PowerShellGet](psget_script_overview.md)
### [Командлеты PowerShellGet для управления сценариями](psget_scriptcmdlets.md)

## [Новые и обновленные командлеты, основанные на отзывах сообщества ](feedback_cmdlets.md)
### [Использование символьных ссылок с помощью командлетов Item](feedback_symbolic.md)
### [Командлеты Archive](feedback_archive.md)
### [Командлеты Clipboard](feedback_clipboard.md)
### [Convert-String](feedback_convertstring.md)
### [Извлечение и анализ структурированных объектов вне строки](feedback_convertfromString.md)
### [Format-Hex](feedback_formathex.md)
### [Параметр NoNewLine](feedback_nonewline.md)
### [New-TemporaryFile](feedback_tempfile.md)
### [New-Guid](feedback_newguid.md)
### [Get-ChildItem получает параметр -Depth](feedback_getchilditem.md)
### [Изменения объекта FileInfo](feedback_fileinfo.md)
### [Поддержка модулей для объявления диапазонов версий (1.* и т. д.)](feedback_moduleversionranges.md)

## [Поток информации](informationstream_overview.md)

## [Создание командлетов PowerShell на основе конечной точки OData](odata_overview.md)

## [Управление сетевыми коммутаторами с помощью PowerShell](networkswitch_overview.md)

## [Инвентаризация программного обеспечения (SIL)](sil_overview.md)

# [Известные проблемы и ограничения](limitation_overview.md)
## [Известные проблемы с настройкой требуемого состояния (DSC)](limitation_dsc.md)


<!--HONumber=May16_HO4-->


