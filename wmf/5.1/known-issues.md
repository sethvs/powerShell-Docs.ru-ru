---
title: "Известные проблемы в WMF 5.1"
ms.date: 2016-07-13
keywords: PowerShell, DSC, WMF
description: 
ms.topic: article
author: krishna
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: b341f57592feb183eb0e7228cdc08460e370369f
ms.sourcegitcommit: f06ef671c0a646bdd277634da89cc11bc2a78a41
translationtype: HT
---
# <a name="known-issues-in-wmf-51"></a>Известные проблемы в WMF 5.1 #

> Примечание. Эта информация может быть изменена.

## <a name="starting-powershell-shortcut-as-administrator"></a>Запуск PowerShell от имени администратора с помощью ярлыка
После установки WMF при попытке запустить PowerShell от имени администратора с помощью ярлыка может появиться сообщение "Неопознанная ошибка".
Повторно запустите PowerShell через ярлык без прав администратора. Теперь он работает и с правами администратора.

## <a name="pester"></a>Pester
В этом выпуске существует две проблемы, которые следует иметь в виду при использовании Pester на сервере Nano.

* Запуск тестов для самого Pester может привести к некоторым ошибкам из-за различий между FULL CLR и CORE CLR. В частности, для типа XmlDocument недоступен метод Validate. Известно, что шесть проверок схемы журналов вывода NUnit завершаются сбоем. 
* Один из тестов объема протестированного кода сейчас завершается сбоем из-за того, что ресурс DSC *WindowsFeature* не существует на сервере Nano Server. Тем не менее эти ошибки обычно носят информационный характер, и их можно спокойно пропустить.

## <a name="operation-validation"></a>Проверка операций 

* Модуль Microsoft.PowerShell.Operation.Validation вызывает ошибку в командлете Update-Help, так как код URI справки не работает.

## <a name="dsc-after-uninstall-wmf"></a>DSC после удаления WMF 
* Удаление WMF не удаляет MOF-документы DSC из папки конфигурации. DSC не будет правильно работать, если MOF-документы содержат более новые свойства, которые недоступны в старых системах. В этом случае запустите скрипт из консоли PowerShell с повышенными правами, чтобы очистить состояния DSC.
 ```PowerShell
    $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
            "$env:windir\system32\configuration\*.mof.checksum",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
           )

    $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
 ```  
