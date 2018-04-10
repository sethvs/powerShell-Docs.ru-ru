---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 3b2c268cd10d7c421b3d1fc73a7bbeaa4714f5fc
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="authoring-improvements-using-powershell-ise"></a><span data-ttu-id="6b9db-102">Усовершенствования создания с помощью интегрированной среды сценариев PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b9db-102">Authoring Improvements using PowerShell ISE</span></span>

<span data-ttu-id="6b9db-103">Создание конфигураций DSC в интегрированной среде сценариев PowerShell стало гораздо проще благодаря следующим усовершенствованиям:</span><span class="sxs-lookup"><span data-stu-id="6b9db-103">Authoring DSC configurations in Windows PowerShell ISE is much easier, thanks to the following improvements:</span></span>

- <span data-ttu-id="6b9db-104">Вывод всех ресурсов DSC в блоке **configuration** или **node** путем нажатия клавиш **CTRL+ПРОБЕЛ** на пустой строке внутри него.</span><span class="sxs-lookup"><span data-stu-id="6b9db-104">List all DSC resources within a **configuration** block or **node** block by entering **Ctrl+Space** on a blank line within it.</span></span>
- <span data-ttu-id="6b9db-105">Автозаполнение свойств ресурсов, имеющих тип **enumeration**.</span><span class="sxs-lookup"><span data-stu-id="6b9db-105">Automatic completion on resource properties that are of the **enumeration** type.</span></span>
- <span data-ttu-id="6b9db-106">Автозаполнение в свойстве **DependsOn** ресурсов DSC, основанное на других экземплярах ресурсов в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6b9db-106">Automatic completion on the **DependsOn** property of DSC resources, based on other resource instances in the configuration.</span></span>
- <span data-ttu-id="6b9db-107">Улучшенное заполнение нажатием клавиши TAB для значений свойств ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6b9db-107">Better tab completion of resource property values.</span></span>

<span data-ttu-id="6b9db-108">**Примечание.** Прежде чем использовать сочетание клавиш CTRL+ПРОБЕЛ для вывода списка параметров, необходимо иметь пустую строку для значений свойств ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6b9db-108">**Note:** You must have an empty string for resource property values before you can use Ctrl+Space to list the options.</span></span> <span data-ttu-id="6b9db-109">Нажатие клавиши **TAB** позволяет переключаться между параметрами.</span><span class="sxs-lookup"><span data-stu-id="6b9db-109">Pressing **Tab** cycles through options.</span></span>