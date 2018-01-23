---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Класс MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: b2d2ce000988f2c10ab04c4ba5a4650bd3c75ec7
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="9014f-103">Класс MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="9014f-103">MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="9014f-104">Локальный диспетчер конфигураций (LCM) управляет состоянием файлов конфигурации и использует агент конфигурации для применения настроек.</span><span class="sxs-lookup"><span data-stu-id="9014f-104">The Local Configuration Manager (LCM) that controls the states of configuration files and uses Configuration Agent to apply the configurations.</span></span>

<span data-ttu-id="9014f-105">Следующий пример синтаксиса — упрощенный MOF-код, который включает все наследуемые свойства.</span><span class="sxs-lookup"><span data-stu-id="9014f-105">The following syntax is simplified from Managed Object Format (MOF) code and includes all of the inherited properties.</span></span>

## <a name="syntax"></a><span data-ttu-id="9014f-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="9014f-106">Syntax</span></span>
------

``` syntax
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## <a name="members"></a><span data-ttu-id="9014f-107">Члены группы</span><span class="sxs-lookup"><span data-stu-id="9014f-107">Members</span></span>
-------

<span data-ttu-id="9014f-108">Класс **MSFT_DSCLocalConfigurationManager** включает следующие члены:</span><span class="sxs-lookup"><span data-stu-id="9014f-108">The **MSFT_DSCLocalConfigurationManager** class has the following members:</span></span>

-   <span data-ttu-id="9014f-109">[Методы][]</span><span class="sxs-lookup"><span data-stu-id="9014f-109">[Methods][]</span></span>

### <a name="methods"></a><span data-ttu-id="9014f-110">Методы</span><span class="sxs-lookup"><span data-stu-id="9014f-110">Methods</span></span>

<span data-ttu-id="9014f-111">Класс **MSFT_DSCLocalConfigurationManager** включает следующие методы:</span><span class="sxs-lookup"><span data-stu-id="9014f-111">The **MSFT_DSCLocalConfigurationManager** class has these methods.</span></span>

|<span data-ttu-id="9014f-112">Метод</span><span class="sxs-lookup"><span data-stu-id="9014f-112">Method</span></span> |<span data-ttu-id="9014f-113">Описание</span><span class="sxs-lookup"><span data-stu-id="9014f-113">Description</span></span> |
|:--- |:---|
| [<span data-ttu-id="9014f-114">ApplyConfiguration</span><span class="sxs-lookup"><span data-stu-id="9014f-114">ApplyConfiguration</span></span>](msft-dsclocalconfigurationmanager-applyconfiguration.md)| <span data-ttu-id="9014f-115">Использует агент конфигурации для применения конфигурации, которая находится в состоянии ожидания.</span><span class="sxs-lookup"><span data-stu-id="9014f-115">Uses the Configuration Agent to apply the configuration that is pending.</span></span>| 
| [<span data-ttu-id="9014f-116">DisableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="9014f-116">DisableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| <span data-ttu-id="9014f-117">Отключает отладку ресурсов DSC.</span><span class="sxs-lookup"><span data-stu-id="9014f-117">Disables DSC resource debugging.</span></span>| 
| [<span data-ttu-id="9014f-118">EnableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="9014f-118">EnableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| <span data-ttu-id="9014f-119">Включает отладку ресурсов DSC.</span><span class="sxs-lookup"><span data-stu-id="9014f-119">Enables DSC resource debugging.</span></span>| 
| [<span data-ttu-id="9014f-120">GetConfiguration</span><span class="sxs-lookup"><span data-stu-id="9014f-120">GetConfiguration</span></span>](msft-dsclocalconfigurationmanager-getconfiguration.md)| <span data-ttu-id="9014f-121">Отправляет документ конфигурации на управляемый узел и использует метод **Get** агента конфигурации для применения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9014f-121">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>| 
| [<span data-ttu-id="9014f-122">GetConfigurationResultOutput</span><span class="sxs-lookup"><span data-stu-id="9014f-122">GetConfigurationResultOutput</span></span>](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| <span data-ttu-id="9014f-123">Получает выходные данные агента конфигурации, относящиеся к определенному заданию.</span><span class="sxs-lookup"><span data-stu-id="9014f-123">Gets the Configuration Agent output relating to a specific job.</span></span>| 
| [<span data-ttu-id="9014f-124">GetConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="9014f-124">GetConfigurationStatus</span></span>](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| <span data-ttu-id="9014f-125">Получает журнал состояния конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9014f-125">Get the configuration status history.</span></span>| 
| [<span data-ttu-id="9014f-126">GetMetaConfiguration</span><span class="sxs-lookup"><span data-stu-id="9014f-126">GetMetaConfiguration</span></span>](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| <span data-ttu-id="9014f-127">Получает параметры локального диспетчера конфигураций, которые используются для управления агентом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9014f-127">Gets the LCM settings that are used to control Configuration Agent.</span></span>| 
| [<span data-ttu-id="9014f-128">PerformRequiredConfigurationChecks</span><span class="sxs-lookup"><span data-stu-id="9014f-128">PerformRequiredConfigurationChecks</span></span>](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| <span data-ttu-id="9014f-129">Запускает проверку согласованности.</span><span class="sxs-lookup"><span data-stu-id="9014f-129">Starts the consistency check.</span></span>| 
| [<span data-ttu-id="9014f-130">RemoveConfiguration</span><span class="sxs-lookup"><span data-stu-id="9014f-130">RemoveConfiguration</span></span>](msft-dsclocalconfigurationmanager-removeconfiguration.md)| <span data-ttu-id="9014f-131">Удаляет файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9014f-131">Removes the configuration files.</span></span>| 
| [<span data-ttu-id="9014f-132">ResourceGet</span><span class="sxs-lookup"><span data-stu-id="9014f-132">ResourceGet</span></span>](msft-dsclocalconfigurationmanager-resourceget.md)| <span data-ttu-id="9014f-133">Напрямую вызывает метод **Get** ресурса DSC.</span><span class="sxs-lookup"><span data-stu-id="9014f-133">Directly calls the **Get** method of a DSC resource.</span></span>| 
| [<span data-ttu-id="9014f-134">ResourceSet</span><span class="sxs-lookup"><span data-stu-id="9014f-134">ResourceSet</span></span>](msft-dsclocalconfigurationmanager-resourceset.md)| <span data-ttu-id="9014f-135">Напрямую вызывает метод **Set** ресурса DSC.</span><span class="sxs-lookup"><span data-stu-id="9014f-135">Directly calls the **Set** method of a DSC resource.</span></span>| 
| [<span data-ttu-id="9014f-136">ResourceTest</span><span class="sxs-lookup"><span data-stu-id="9014f-136">ResourceTest</span></span>](msft-dsclocalconfigurationmanager-resourcetest.md)| <span data-ttu-id="9014f-137">Напрямую вызывает метод **Test** ресурса DSC.</span><span class="sxs-lookup"><span data-stu-id="9014f-137">Directly calls the **Test** method of a DSC resource.</span></span>| 
| [<span data-ttu-id="9014f-138">RollBack</span><span class="sxs-lookup"><span data-stu-id="9014f-138">RollBack</span></span>](msft-dsclocalconfigurationmanager-rollback.md)| <span data-ttu-id="9014f-139">Выполняет откат к предыдущей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9014f-139">Rolls back to a previous configuration.</span></span>| 
| [<span data-ttu-id="9014f-140">SendConfiguration</span><span class="sxs-lookup"><span data-stu-id="9014f-140">SendConfiguration</span></span>](msft-dsclocalconfigurationmanager-sendconfiguration.md)| <span data-ttu-id="9014f-141">Отправляет документ конфигурации на управляемый узел и сохраняет его как ожидающее изменение.</span><span class="sxs-lookup"><span data-stu-id="9014f-141">Sends the configuration document to the managed node and saves it as a pending change.</span></span>| 
| [<span data-ttu-id="9014f-142">SendConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="9014f-142">SendConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| <span data-ttu-id="9014f-143">Отправляет документ конфигурации на управляемый узел и использует агент конфигурации для применения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9014f-143">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>| 
| [<span data-ttu-id="9014f-144">SendConfigurationApplyAsync</span><span class="sxs-lookup"><span data-stu-id="9014f-144">SendConfigurationApplyAsync</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| <span data-ttu-id="9014f-145">Отправляет документ конфигурации на управляемый узел и запускает агент конфигурации для применения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9014f-145">Send the configuration document to the managed node and start using the Configuration Agent to apply the configuration.</span></span> <span data-ttu-id="9014f-146">Для получения выходных данных используется метод GetConfigurationResultOutput.</span><span class="sxs-lookup"><span data-stu-id="9014f-146">Use GetConfigurationResultOutput to retrieve result output.</span></span>| 
| [<span data-ttu-id="9014f-147">SendMetaConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="9014f-147">SendMetaConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| <span data-ttu-id="9014f-148">Задает параметры локального диспетчера конфигураций, которые используются для управления агентом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9014f-148">Sets the LCM settings that are used to control the Configuration Agent.</span></span>| 
| [<span data-ttu-id="9014f-149">StopConfiguration</span><span class="sxs-lookup"><span data-stu-id="9014f-149">StopConfiguration</span></span>](msft-dsclocalconfigurationmanager-stopconfiguration.md)| <span data-ttu-id="9014f-150">Останавливает выполняемую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="9014f-150">Stops the configuration that is in progress.</span></span>| 
| [<span data-ttu-id="9014f-151">TestConfiguration</span><span class="sxs-lookup"><span data-stu-id="9014f-151">TestConfiguration</span></span>](msft-dsclocalconfigurationmanager-testconfiguration.md)| <span data-ttu-id="9014f-152">Отправляет документ конфигурации на управляемый узел и проверяет соответствие текущей конфигурации документу.</span><span class="sxs-lookup"><span data-stu-id="9014f-152">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>| 



 

## <a name="requirements"></a><span data-ttu-id="9014f-153">Требования</span><span class="sxs-lookup"><span data-stu-id="9014f-153">Requirements</span></span>
------------
><span data-ttu-id="9014f-154">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="9014f-154">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="9014f-155">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="9014f-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>



 

 



