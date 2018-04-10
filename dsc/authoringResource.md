---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Создание пользовательских ресурсов настройки требуемого состояния Windows PowerShell
ms.openlocfilehash: 7da4741a773d40da75c6ef667c35f86e1bae74bf
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="build-custom-windows-powershell-desired-state-configuration-resources"></a><span data-ttu-id="d3237-103">Создание пользовательских ресурсов настройки требуемого состояния Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3237-103">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>

> <span data-ttu-id="d3237-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="d3237-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="d3237-105">Настройка требуемого состояния (DSC) Windows PowerShell включает встроенные ресурсы для настройки среды.</span><span class="sxs-lookup"><span data-stu-id="d3237-105">Windows PowerShell Desired State Configuration (DSC) has built-in resources that you can use to configure your environment.</span></span> <span data-ttu-id="d3237-106">(Дополнительные сведения см. в статье [Встроенные ресурсы настройки требуемого состояния (DSC) Windows PowerShell](builtInResource.md).) Этот раздел содержит сведения о разработке ресурсов и ссылок на разделы с описанием особенностей и примерами.</span><span class="sxs-lookup"><span data-stu-id="d3237-106">(For more information, see [Built-In Windows PowerShell Desired State Configuration Resources](builtInResource.md).) This topic provides an overview of developing resources and links to topics with specific information and examples.</span></span>

## <a name="dsc-resource-components"></a><span data-ttu-id="d3237-107">Компоненты ресурсов DSC</span><span class="sxs-lookup"><span data-stu-id="d3237-107">DSC resource components</span></span>

<span data-ttu-id="d3237-108">Ресурс DSC — это модуль Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3237-108">A DSC resource is a Windows PowerShell module.</span></span> <span data-ttu-id="d3237-109">Модуль содержит схему (определение настраиваемых свойств) и реализацию (код, выполняющий заданную конфигурацией работу) для ресурса.</span><span class="sxs-lookup"><span data-stu-id="d3237-109">The module contains both the schema (the definition of the configurable properties) and the implementation (the code that does the actual work specified by a configuration) for the resource.</span></span> <span data-ttu-id="d3237-110">Схема ресурсов DSC может быть определена в MOF-файле, а реализация выполняется модулем сценариев.</span><span class="sxs-lookup"><span data-stu-id="d3237-110">A DSC resource schema can be defined in a MOF file, and the implementation is performed by a script module.</span></span> <span data-ttu-id="d3237-111">С добавлением поддержки классов PowerShell в версии 5 появилась возможность определять схему и реализацию в классе.</span><span class="sxs-lookup"><span data-stu-id="d3237-111">Beginning with the support of PowerShell classes in version 5, the schema and implementation can both be defined in a class.</span></span> <span data-ttu-id="d3237-112">Более подробные инструкции по созданию ресурсов DSC см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="d3237-112">The following topics describe in more detail how to create DSC resources.</span></span>

* [<span data-ttu-id="d3237-113">Написание пользовательских ресурсов DSC с использованием MOF</span><span class="sxs-lookup"><span data-stu-id="d3237-113">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
* [<span data-ttu-id="d3237-114">Реализация ресурса DSC на языке C#</span><span class="sxs-lookup"><span data-stu-id="d3237-114">Implementing a DSC resource in C#</span></span>](authoringResourceMofCS.md)
* [<span data-ttu-id="d3237-115">Написание пользовательских ресурсов DSC с использованием классов PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3237-115">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)
* [<span data-ttu-id="d3237-116">Составные ресурсы: использование конфигурации DSC как ресурса</span><span class="sxs-lookup"><span data-stu-id="d3237-116">Composite resources: Using a DSC configuration as a resource</span></span>](authoringResourceComposite.md)
* [<span data-ttu-id="d3237-117">Использование конструктора ресурсов</span><span class="sxs-lookup"><span data-stu-id="d3237-117">Using the Resource Designer tool</span></span>](authoringResourceMofDesigner.md)