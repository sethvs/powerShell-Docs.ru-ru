# Логика для подготовки зависимостей модуля во время операции публикации
1.  Модули, перечисленные в списке RequiredModules, считаются зависимостями.
2.  Модули, перечисленные в списке NestedModules, база модуля которых не находится под указанной базой модуля, считаются зависимостями.

3.  Указанные выше зависимости должны быть доступны в том же целевом репозитории, иначе операция публикации приведет к ошибке.
    Например, если SnippetPx недоступен в репозитории, возникнет следующая ошибка.
    ```powershell
    Publish-PSArtifactUtility : PowerShellGet cannot resolve the module dependency 'SnippetPx' of the module 'TypePx' on the repository 'LocalRepo'. Verify that the dependent module 'SnippetPx' is available in the repository 'LocalRepo'. If this dependent
    'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```
4.  Некоторые зависимости модуля могут управляться извне; в этом случае они должны добавляться в запись ExternalModuleDependencies раздела PSData манифеста модуля.
    Ниже приводится часть вышеупомянутого сообщения об ошибке
    ```powershell
    If this dependent 'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```

*Во время установки модуля подготовленный выше список зависимостей используется для установки зависимостей.*

*Убедитесь, что зависимости вашего модуля доступны в разделе $env:PSModulePath в системе во время операции публикации.*


<!--HONumber=Aug16_HO3-->


