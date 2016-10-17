# Элементы с совместимыми выпусками PowerShell
Начиная с версии 5.1 доступны различные выпуски среды PowerShell, что означает различные наборы возможностей и совместимость с разными платформами.

- **Выпуск Desktop Edition:** построен на основе .NET Framework и обеспечивает совместимость со скриптами и модулями, которые предназначены для версий PowerShell, выполняющихся в полноценных выпусках Windows, таких как Server Core и Windows Desktop.
- **Выпуск Core Edition:** построен на основе .NET Core и обеспечивает совместимость со скриптами и модулями, которые предназначены для версий PowerShell, выполняющихся в выпусках Windows с ограниченными возможностями, таких как Nano Server и Windows IoT.

## Коллекция PowerShell извлекает поддерживаемые метаданные PSEditions и позволяет отфильтровывать элементы, совместимые с конкретными выпусками PowerShell

Если элемент имеет указанные совместимые версии PSEdition, они будут перечислены в разделе "Выпуски PowerShell" на странице отображения элемента, а также в результатах элементов.
![Страница отображения элемента с выпусками PSEdition](Images/ItemDisplayPageWithPSEditions.PNG)

## Поиск элементов в коллекции пользовательского интерфейса, работающих в PowerShellCore
Для фильтрации элементов в коллекции PowerShell используйте Tags:"PSEdition_Desktop" и Tags:"PSEdition_Core".

### Для поиска элементов, совместимых с выпуском PowerShell Core, используйте Tags:"PSEdition_Core".
![Результаты поиска элементов, совместимых с Core PSEdition](Images/SearchResultsWithPSEditions.PNG)

### Для поиска элементов, совместимых с выпуском PowerShell Desktop, используйте Tags:"PSEdition_Desktop".
![Результаты поиска элементов, совместимых с Desktop PSEdition](Images/SearchResultsWithPSEdition_Desktop.PNG)

## Дополнительные сведения о разработке и поиске элементов с совместимыми выпусками PowerShell
### [Модули с PSEditions](../psget/module/modulewithpseditionsupport.md)
### [Скрипты с PSEditions](../psget/script/scriptwithpseditionsupport.md)

<!--HONumber=Aug16_HO3-->


