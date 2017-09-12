---
ms.date: 2017-08-25
keywords: "powershell,командлет"
title: "Объект ObjectModelRoot"
ms.openlocfilehash: eb3424ff147c35364fa08543d59ebd30f6d2d857
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2017
---
# <a name="the-objectmodelroot-object"></a>Объект ObjectModelRoot

Объект **$PsISE**, который является основным корневым объектом в интегрированной среде скриптов Windows PowerShell® (ISE), — это экземпляр класса Microsoft.PowerShell.Host.ISE.ObjectModelRoot.
В этом разделе описаны свойства объекта **ObjectModelRoot**.

## <a name="properties"></a>Свойства

### <a name="currentfile"></a>CurrentFile

> Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

Свойство только для чтения, которое получает файл, связанный с этим объектом узла, находящимся в данный момент в фокусе.

### <a name="currentpowershelltab"></a>CurrentPowerShellTab

> Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает вкладку PowerShell, находящуюся в фокусе.

### <a name="currentvisiblehorizontaltool"></a>CurrentVisibleHorizontalTool

> Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает видимую в данный момент надстройку интегрированной среды сценариев Windows PowerShell, которая находится в горизонтальной области инструментов в нижней части редактора.

### <a name="currentvisibleverticaltool"></a>CurrentVisibleVerticalTool

> Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

Свойство только для чтения, которое получает видимую в данный момент надстройку интегрированной среды сценариев Windows PowerShell, которая находится в вертикальной области инструментов в правой части редактора.

### <a name="options"></a>Параметры

> Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

Свойство только для чтения, которое получает различные параметры, изменяющие настройки в интегрированной среде сценариев Windows PowerShell.

### <a name="powershelltabs"></a>PowerShellTabs

> Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

Свойство только для чтения, которое получает коллекцию вкладок PowerShell, открытых в интегрированной среде сценариев Windows PowerShell. По умолчанию этот объект содержит одну вкладку PowerShell. Тем не менее можно добавить в этот объект больше вкладок PowerShell с помощью сценариев или меню в интегрированной среде сценариев Windows PowerShell.

## <a name="see-also"></a>См. также

- [Объектная модель скриптов интегрированной среды скриптов Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Справочник по объектной модели интегрированной среды скриптов Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [Иерархия объектной модели интегрированной среды скриптов](The-ISE-Object-Model-Hierarchy.md)
