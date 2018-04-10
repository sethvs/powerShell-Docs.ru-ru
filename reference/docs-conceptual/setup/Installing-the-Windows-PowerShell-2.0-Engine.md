---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Установка подсистемы Windows PowerShell 2.0
ms.assetid: 82928f2b-f96a-4ae6-a0d0-6e7b181da308
ms.openlocfilehash: 0b3282a1a67886509e749af0f499c47fe7a99411
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="installing-the-windows-powershell-20-engine"></a>Установка подсистемы Windows PowerShell 2.0
В этом разделе описывается установка модуля Windows PowerShell 2.0.

Windows PowerShell 3.0 предназначен для обратной совместимости с Windows PowerShell 2.0. Командлеты, поставщики, оснастки, модули и сценарии, написанные для Windows PowerShell 2.0, выполняются и в Windows PowerShell 3.0, и Windows PowerShell 4.0 без изменений. Однако из-за изменений в политике активации среды выполнения в Microsoft .NET Framework 4 основные программы Windows PowerShell, написанные для Windows PowerShell 2.0 и скомпилированные с помощью среды CLR 2.0, не могут выполняться в последующих выпусках Windows PowerShell 4.0, компилируемых в среде CLR 2.0, без изменений.

Чтобы обеспечить обратную совместимость с командами и основными программами, которые были затронуты этими изменениями, подсистемы Windows PowerShell 2.0, Windows PowerShell 3.0 и Windows PowerShell 4.0 рассчитаны на параллельное выполнение. Кроме того, подсистема Windows PowerShell 2.0 входит в Windows Server 2012 R2, Windows 8.1, Windows 8, Windows Server 2012 и Windows Management Framework 3.0. Подсистема Windows PowerShell 2.0 предназначена для использования только в том случае, если выполнение существующего сценария или существующей основной программы невозможно из-за несовместимости с Windows PowerShell 3.0, Windows PowerShell 4.0 или Microsoft .NET Framework 4. Такие ситуации довольно редки.

Обработчик Windows PowerShell 2.0 представляет собой дополнительный компонент Windows Server 2012 R2, Windows 8.1, Windows® 8 и Windows Server® 2012. В более ранних версиях Windows при установке Windows Management Framework 3.0 установка Windows PowerShell 3.0 полностью заменяет установку Windows PowerShell 2.0 в каталоге установки Windows PowerShell. При этом подсистема Windows PowerShell 2.0 сохраняется.

Дополнительные сведения о запуске подсистемы Windows PowerShell 2.0 см. в статье [Запуск подсистемы Windows PowerShell 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="on-windows-81-and-windows-8"></a>Windows 8.1 и Windows 8
В Windows 8.1 и Windows 8 функция подсистемы Windows PowerShell 2.0 по умолчанию включена. Однако для его использования следует включить параметр для необходимой ему платформы Microsoft .NET Framework 3.5. Этот раздел также поясняет, как включать и отключить компонент подсистемы Windows PowerShell 2.0.

#### <a name="to-turn-on-net-framework-35"></a>Включение .NET Framework 3.5

1. На экране **Пуск** введите **компоненты Windows**.

2. В панели **Приложения** щелкните **Параметры**, а затем выберите **Включение или отключение компонентов Windows**.

3. В поле **Компоненты Windows** выберите элемент **.NET Framework 3.5 (включает .NET 2.0 и 3.0)**.

    При выборе элемента **.NET Framework 3.5 (включает .NET 2.0 и 3.0)** поле заливается, указывая, что выбрана только часть компонента. Этого достаточно для подсистемы Windows PowerShell 2.0.

#### <a name="to-turn-the-windows-powershell-20-engine-on-and-off"></a>Включение и отключение подсистемы Windows PowerShell 2.0

1. На экране **Пуск** введите **компоненты Windows**.

2. В панели **Приложения** щелкните **Параметры**, а затем выберите **Включение или отключение компонентов Windows**.

3. В поле **Компоненты Windows** разверните узел **Windows PowerShell 2.0** и установите либо снимите флажок **Windows PowerShell 2.0 Engine**.

## <a name="on-windows-server-2012-r2-and-windows-server-2012"></a>Windows Server 2012 или Windows Server 2012 R2
Для добавления подсистемы Windows PowerShell 2.0 и компонентов Microsoft .NET Framework 3.5 используйте описанные ниже процедуры. Подсистеме Windows PowerShell 2.0 требуется Microsoft .NET Framework версии не ниже 2.0.50727. Этому требованию удовлетворяет Microsoft .NET Framework 3.5.

#### <a name="to-add-the-net-framework-35-feature"></a>Добавление компонента .NET Framework 3.5

1. В меню **Управление** **диспетчера сервера** выберите **Добавить роли и компоненты**.

    Можно также щелкнуть **Все серверы** в **диспетчере сервера**, щелкнуть имя сервера правой кнопкой мыши и выбрать **Добавить роли и компоненты**.

2. На странице **Тип установки** выберите **Установка ролей или компонентов**.

3. На странице **Компоненты** разверните узел **Компоненты .NET Framework 3.5** и выберите команду **.NET Framework 3.5 (включает .NET 2.0 и 3.0)**.

    Другие параметры в этом узле для подсистемы Windows PowerShell 2.0 не требуются.

#### <a name="to-add-the-windows-powershell-20-engine-feature"></a>Добавление функции подсистемы Windows PowerShell 2.0

- В меню **Управление** **диспетчера сервера** выберите **Добавить роли и компоненты**.

    Можно также щелкнуть **Все серверы** в **диспетчере сервера**, щелкнуть имя сервера правой кнопкой мыши и выбрать **Добавить роли и компоненты**.

- На странице **Тип установки** выберите **Установка ролей или компонентов**.

- На странице **Компоненты** раскройте **Windows PowerShell (установлено)** и выберите пункт **Подсистема Windows PowerShell 2.0**.

Дополнительные сведения о запуске подсистемы Windows PowerShell 2.0 см. в статье [Запуск подсистемы Windows PowerShell 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="on-earlier-systems"></a>В предыдущих версиях систем
Пакет [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881), устанавливающий Windows PowerShell 4.0 в Windows 7, Windows Server 2008 R2 и Windows Server 2012, включает подсистему Windows PowerShell 2.0. Подсистема Windows PowerShell 2.0 включена и готова к использованию без дополнительной установки, настройки или конфигурации.

Пакет Windows Management Framework 3.0, устанавливающий Windows PowerShell 3.0 в Windows 7, Windows Server 2008 R2 и Windows Server 2008, включает подсистему Windows PowerShell 2.0. Подсистема Windows PowerShell 2.0 включена и готова к использованию без дополнительной установки, настройки или конфигурации.

## <a name="see-also"></a>См. также
- [Требования Windows PowerShell к системе](Windows-PowerShell-System-Requirements.md)
- [Установка Windows PowerShell](Installing-Windows-PowerShell.md)
- [Запуск Windows PowerShell](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)
- [Запуск подсистемы Windows PowerShell 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md)