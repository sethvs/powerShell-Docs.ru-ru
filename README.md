## <a name="microsoft-open-source-code-of-conduct"></a>Правила поведения: использование открытого исходного кода Майкрософт

Этот проект основывается на [правилах использования открытого исходного кода Майкрософт](https://opensource.microsoft.com/codeofconduct/).
Дополнительные сведения см. в [вопросах и ответах о правилах поведения](https://opensource.microsoft.com/codeofconduct/faq/) или обратитесь по адресу [opencode@microsoft.com](mailto:opencode@microsoft.com) с любыми дополнительными вопросами или комментариями.

[![Состояние сборки](https://ci.appveyor.com/api/projects/status/onshefxnc4g4pv87/branch/staging?svg=true)](https://ci.appveyor.com/project/PowerShell/powershell-docs/branch/staging)

# <a name="powershell-documentation"></a>Документация по PowerShell

Добро пожаловать в репозиторий PowerShell-Docs, в котором находится официальная документация по Windows PowerShell. 

## <a name="repository-structure"></a>Структура репозитория
Для каждой папки в этом репозитории предусмотрена публикация на сайте [MSDN](https://msdn.microsoft.com/en-us/powershell). Папки соответствуют следующим ресурсам PowerShell:
* [/dsc/](https://msdn.microsoft.com/en-us/powershell/dsc/) — для функции настройки требуемого состояния;
* [/gallery/](https://msdn.microsoft.com/powershell/gallery) — для [коллекции PowerShell](https://www.powershellgallery.com/);
* [/jea/](https://msdn.microsoft.com/powershell/jea/) — для функции Just Enough Administration (JEA);
* [/reference/](https://msdn.microsoft.com/powershell/reference/) — справочник по модулям PowerShell версий 2.0, 3.0, 4.0, 5.0, 5.1 и 6.0
  * (в будущем это содержимое можно будет получать с помощью командлета `Get-Help`);
* [/scripting/](https://msdn.microsoft.com/en-us/powershell/scripting/) — общие справочные сведения о PowerShell;
* [/wmf](https://msdn.microsoft.com/en-us/powershell/wmf/readme) — содержит заметки о платформе Windows Management Framework (пакет, используемый для распространения новых версий PowerShell в предыдущих версиях Windows). 



## <a name="contributing"></a>Публикация

Мы активно объединяем публикации в этом репозитории с помощью [запроса на включение внесенных изменений](https://help.github.com/articles/using-pull-requests/) в *промежуточной* ветви. Примечание. Для того, чтобы сообщество свободно использовало ваши публикации, перед отправкой запроса на включение внесенных изменений необходимо [подписать соглашение Contribution License Agreement](https://cla.microsoft.com/).
Дополнительные сведения о публикации можно прочесть в [руководстве по публикациям](CONTRIBUTING.md).
Также доступен черновой вариант [руководства по стилю](./STYLE.md). Вы можете ознакомиться с ним, прежде чем вносить предложения.
Используйте шаблоны "Проблема" и "Запрос на включение внесенных изменений", чтобы обеспечить согласованность документации по разным версиям. 
