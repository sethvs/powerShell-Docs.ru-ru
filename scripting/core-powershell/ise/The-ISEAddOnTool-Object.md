---
title:  Объект ISEAddOnTool
ms.date:  2016-05-11
keywords:  powershell,cmdlet
description:  
ms.topic:  article
author:  jpjofre
manager:  dongill
ms.prod:  powershell
ms.assetid:  ce84d8bc-07ba-41f6-bdde-d6f3fddcd1e3
---

# Объект ISEAddOnTool
  Объект **ISEAddonTool** — это устанавливаемая надстройка, расширяющая функциональные возможности интегрированной среды сценариев ISE. В качестве примера можно привести средство **Commands**, которое отображается, если выбрать **Вид**, а затем **Показать настройку Command**. После этого средство становится доступным за счет манипуляций с различными доступными объектами **ISEAddOnTool**.

 Каждую надстройку можно связать с вертикальной или с горизонтальной панелью. Вертикальная область прикрепляется к правому краю интегрированной среды сценариев Windows PowerShell. Горизонтальная панель прикрепляется к нижнему краю.

 Каждая вкладка PowerShell в интегрированной среде сценариев Windows PowerShell может содержать собственный набор установленных надстроек. Доступ к коллекции средств, доступных для выбранной вкладки, или к свойствам одного из объектов **PowerShellTab** в объекте коллекции [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) рассматривается в статьях [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-ISEAddOnToolCollection-Object.md) и [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-ISEAddOnToolCollection-Object.md).

## Методы
 Для объектов этого класса нет доступных методов интегрированной среды сценариев Windows PowerShell.

## Свойства

###  <a name="Control"></a> Элемент
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

 Свойство **Control** обеспечивает доступ для чтения к множеству сведений надстройки Command.

```
# View the properties of the Commands add-on tool.
# (assumes that it is visible in the vertical pane)
$psISE.CurrentVisibleVerticalTool.Control
HostObject                  : Microsoft.PowerShell.Host.ISE.ObjectModelRoot
Content                     :
HasContent                  :
ContentTemplate             :
ContentTemplateSelector     :
ContentStringFormat         :
BorderBrush                 :
BorderThickness             :
Background                  :
Foreground                  :
FontFamily                  :
FontSize                    :
FontStretch                 :
FontStyle                   :
FontWeight                  :
HorizontalContentAlignment  :
VerticalContentAlignment    :
TabIndex                    :
IsTabStop                   :
Padding                     :
Template                    : System.Windows.Controls.ControlTemplate
Style                       :
OverridesDefaultStyle       :
UseLayoutRounding           :
Triggers                    : {}
TemplatedParent             :
Resources                   : {System.Windows.Controls.TabItem}
DataContext                 :
BindingGroup                :
Language                    :
Name                        :
Tag                         :
InputScope                  :
ActualWidth                 : 370.75
ActualHeight                : 676.559097412109
LayoutTransform             :
Width                       :
MinWidth                    :
MaxWidth                    :
Height                      :
MinHeight                   :
MaxHeight                   :
FlowDirection               : LeftToRight
Margin                      :
HorizontalAlignment         :
VerticalAlignment           :
FocusVisualStyle            :
Cursor                      :
ForceCursor                 :
IsInitialized               : True
IsLoaded                    :
ToolTip                     :
ContextMenu                 :
Parent                      :
HasAnimatedProperties       :
InputBindings               :
CommandBindings             :
AllowDrop                   :
DesiredSize                 : 227.66,676.559097412109
IsMeasureValid              : True
IsArrangeValid              : True
RenderSize                  : 370.75,676.559097412109
RenderTransform             :
RenderTransformOrigin       :
IsMouseDirectlyOver         : False
IsMouseOver                 : False
IsStylusOver                : False
IsKeyboardFocusWithin       : False
IsMouseCaptured             :
IsMouseCaptureWithin        : False
IsStylusDirectlyOver        : False
IsStylusCaptured            :
IsStylusCaptureWithin       : False
IsKeyboardFocused           : False
IsInputMethodEnabled        :
Opacity                     :
OpacityMask                 :
BitmapEffect                :
Effect                      :
BitmapEffectInput           :
CacheMode                   :
Uid                         :
Visibility                  : Visible
ClipToBounds                : False
Clip                        :
SnapsToDevicePixels         : False
IsFocused                   :
IsEnabled                   :
IsHitTestVisible            :
IsVisible                   : True
Focusable                   :
PersistId                   : 1
IsManipulationEnabled       :
AreAnyTouchesOver           : False
AreAnyTouchesDirectlyOver   :
AreAnyTouchesCapturedWithin : False
AreAnyTouchesCaptured       :
TouchesCaptured             : {}
TouchesCapturedWithin       : {}
TouchesOver                 : {}
TouchesDirectlyOver         : {}
DependencyObjectType        : System.Windows.DependencyObjectType
IsSealed                    : False
Dispatcher                  : System.Windows.Threading.Dispatcher

```

###  <a name="IsVisible"></a> IsVisible
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

 Логическое свойство, которое определяет видимость настройки на соответствующей области. Если она видна, свойству **IsVisible** можно присвоить значение **$false**, чтобы скрыть средство, или ******$true**, чтобы оно отображалось на вкладке PowerShell. Обратите внимание на то, что к скрытой надстройке нельзя получить доступ с помощью объекта **CurrentVisibleHorizontalTool** или **CurrentVisibleVerticalTool**, а значит, ее нельзя сделать видимой, используя данное свойство объекта.

```
# Hide the current tool in the vertical tool pane
$psISE.CurrentVisibleVerticalTool.IsVisible = $false
# Show the first tool on the currently selected PowerShell tab
$psISE.CurrentPowerShellTab.VerticalAddOnTools[0].IsVisible=$true

```

###  <a name="name"></a> Название
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

 Свойство только для чтения, которое получает имя оснастки.

```
# Gets the name of the visible vertical pane add-on tool.
$psISE.CurrentVisibleVerticalTool.name
Commands

```

## См. также
 [Объект ISEAddOnToolCollection](The-ISEAddOnToolCollection-Object.md)
 [Объектная модель сценариев интегрированной среды сценариев Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
 [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md)
 [Иерархия объектной модели интегрированной среды сценариев](The-ISE-Object-Model-Hierarchy.md)



<!--HONumber=May16_HO2-->


