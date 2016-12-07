---
title: "Прямой вызов методов ресурсов DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 97d97a36830088d6ee1296cda5310e087fc41893
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="calling-dsc-resource-methods-directly"></a>Прямой вызов методов ресурсов DSC

>Область применения: Windows PowerShell 5.0

Командлет [Invoke-DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx) можно использовать для прямого вызова функций или методов ресурса DSC (функций **Get-TargetResource**, **Set-TargetResource** и **Test-TargetResource** ресурса на основе MOF-файла или методов **Get**, **Set** и **Test** ресурса на основе класса). Этот командлет могут использовать сторонние разработчики, которым требуется использовать ресурсы DSC, кроме того, он удобен для разработки ресурсов. 

Командлет обычно используется в сочетании со свойством метаконфигурации `refreshMode = 'Disabled'`, однако он доступен независимо от значения **refreshMode**.

При вызове командлета **Invoke-DscResource** указать, какой метод или функцию необходимо вызвать, можно с помощью параметра **Method**. Свойства ресурса указываются путем передачи хэш-таблицы в качестве значения параметра **Property**.

Ниже приведены примеры прямого вызова методов ресурсов:

## <a name="ensure-a-file-is-present"></a>Проверка наличия файла

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a>Тестирование наличия файла

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a>Получение содержимого файла

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

>**Примечание**. Прямой вызов методов составного ресурса не поддерживается. Вместо этого вызывайте методы базовых ресурсов, входящих в составной ресурс.

## <a name="see-also"></a>См. также
- [Написание пользовательских ресурсов DSC с использованием MOF](authoringResourceMOF.md) 
- [Написание пользовательских ресурсов DSC с использованием классов PowerShell](authoringResourceClass.md)
- [Отладка ресурсов DSC](debugResource.md)

