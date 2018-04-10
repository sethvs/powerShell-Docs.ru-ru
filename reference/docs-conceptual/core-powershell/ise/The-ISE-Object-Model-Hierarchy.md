---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Иерархия объектной модели интегрированной среды сценариев
ms.openlocfilehash: 0159707b1050c412a74da3d3ca02a46cea982556
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="the-ise-object-model-hierarchy"></a>Иерархия объектной модели интегрированной среды сценариев

В этом разделе демонстрируется иерархия объектов, которые входят в состав интегрированной среды сценариев Windows PowerShell (ISE).
Интегрированная среда сценариев Windows PowerShell входит в состав Windows PowerShell 3.0 и Windows PowerShell 4.0.
Щелкните объект, чтобы перейти к справочной документации для класса, определяющего объект.

## <a name="psise-object"></a>Объект $psISE

Объект **$psISE** — это [корневой объект](The-ObjectModelRoot-Object.md) иерархии объектов интегрированной среды сценариев Windows PowerShell.
Располагаясь на верхнем уровне, он предоставляет доступ к следующим объектам для создания сценариев:

## <a name="psisecurrentfilethe-isefile-objectmd"></a>[$psISE.CurrentFile](The-ISEFile-Object.md)

Объект **$PsISE.CurrentFile** является экземпляром класса [ISEFile](The-ISEFile-Object.md).

## <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a>[$psISE.CurrentPowerShellTab](The-PowerShellTab-Object.md)

Объект **$psISE.CurrentPowerShellTab** является экземпляром класса [PowerShellTab](The-PowerShellTab-Object.md).

## <a name="psisecurrentvisiblehorizontaltool"></a>$psISE.CurrentVisibleHorizontalTool

Объект **$PsISE.CurrentVisibleHorizontalTool** является экземпляром класса [ISEAddOnTool](The-ISEAddOnTool-Object.md).
Он представляет установленную надстройку, закрепленную в верхней части окна интегрированной среды сценариев Windows PowerShell.

## <a name="psisecurrentvisibleverticaltool"></a>$psISE.CurrentVisibleVerticalTool

Объект **$PsISE.CurrentVisibleHorizontalTool** является экземпляром класса [ISEAddOnTool](The-ISEAddOnTool-Object.md).
Он представляет установленную надстройку, закрепленную в правой части окна интегрированной среды сценариев Windows PowerShell.

## <a name="psiseoptionsthe-iseoptions-objectmd"></a>[$psISE.Options](The-ISEOptions-Object.md)

Объект **$PsISE.Options** является экземпляром класса [ISEOptions](The-ISEOptions-Object.md).
Объект ISEOptions представляет различные параметры для интегрированной среды сценариев Windows PowerShell.
Он является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEOptions.

## <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a>[$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md)

Объект **$PsISE.PowerShellTabs** является экземпляром класса [PowerShellTabCollection](The-PowerShellTabCollection-Object.md).
Это коллекция всех открытых вкладок PowerShell, представляющих доступные среды выполнения Windows PowerShell на локальном компьютере или на подключенных удаленных компьютерах.
Каждый элемент в коллекции является экземпляром класса [PowerShellTab](The-PowerShellTab-Object.md).

## <a name="see-also"></a>См. также

- [Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Иерархия объектной модели интегрированной среды скриптов](The-ISE-Object-Model-Hierarchy.md)