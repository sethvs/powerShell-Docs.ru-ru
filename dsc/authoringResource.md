---
title: "Создание пользовательских ресурсов настройки требуемого состояния Windows PowerShell"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: fe2697de322be99e9b5dfe79090fda4082a73623
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="build-custom-windows-powershell-desired-state-configuration-resources"></a>Создание пользовательских ресурсов настройки требуемого состояния Windows PowerShell

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Настройка требуемого состояния (DSC) Windows PowerShell включает встроенные ресурсы для настройки среды. (Дополнительные сведения см. в статье [Встроенные ресурсы настройки требуемого состояния (DSC) Windows PowerShell](builtInResource.md).) Этот раздел содержит сведения о разработке ресурсов и ссылок на разделы с описанием особенностей и примерами.

## <a name="dsc-resource-components"></a>Компоненты ресурсов DSC

Ресурс DSC — это модуль Windows PowerShell. Модуль содержит схему (определение настраиваемых свойств) и реализацию (код, выполняющий заданную конфигурацией работу) для ресурса. Схема ресурсов DSC может быть определена в MOF-файле, а реализация выполняется модулем сценариев. С добавлением поддержки классов PowerShell в версии 5 появилась возможность определять схему и реализацию в классе. Более подробные инструкции по созданию ресурсов DSC см. в следующих статьях:

* [Написание пользовательских ресурсов DSC с использованием MOF](authoringResourceMOF.md) 
* [Реализация ресурса DSC на языке C#](authoringResourceMofCS.md) 
* [Написание пользовательских ресурсов DSC с использованием классов PowerShell](authoringResourceClass.md) 
* [Составные ресурсы: использование конфигурации DSC как ресурса](authoringResourceComposite.md) 
* [Использование конструктора ресурсов](authoringResourceMofDesigner.md) 

