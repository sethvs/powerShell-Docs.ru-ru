---
ms.date: 03/15/2018
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Использование DSC в Microsoft Azure
ms.openlocfilehash: 5b0d577e1fecdeac38c2c5f8e955a2d23b1eb707
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="using-dsc-on-microsoft-azure"></a>Использование DSC в Microsoft Azure

Настройка требуемого состояния (DSC) поддерживается в Microsoft Azure при помощи [обработчика расширений настройки требуемого состояния Azure](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview) и [DSC в службе автоматизации Azure](/azure/automation/automation-dsc-overview).

## <a name="azure-desired-state-configuration-extension-handler"></a>Обработчик расширения настройки требуемого состояния Azure

Расширение Azure DSC позволяет управлять виртуальными машинами, размещенным в Microsoft Azure, при помощи DSC.
Дополнительные сведения см. в следующих разделах:

- [Обработчик расширения настройки требуемого состояния Azure](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview)
- [Windows VMSS и настройка требуемого состояния при помощи шаблонов Azure Resource Manager](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-template)
- [Передача учетных данных в обработчик расширения настройки требуемого состояния Azure](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-credentials)
- [Журнал расширения Azure Desired State Configuration](azureDscexthistory.md)

## <a name="azure-automation-dsc"></a>DSC в службе автоматизации Azure

[Служба автоматизации Azure](https://azure.microsoft.com/services/automation/) позволяет управлять конфигурациями DSC, ресурсами и управляемыми узлами из Azure. Дополнительные сведения см. в следующих разделах:

- [DSC в службе автоматизации Azure](/azure/automation/automation-dsc-overview)
- [Начало работы с DSC в службе автоматизации Azure](/azure/automation/automation-dsc-getting-started)
- [Подключение компьютеров для управления при помощи DSC в службе автоматизации Azure](/azure/automation/automation-dsc-onboarding)