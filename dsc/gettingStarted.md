---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Начало работы с настройкой требуемого состояния PowerShell
ms.openlocfilehash: b5aff5008db5a5e45b77d8094b0e48ad98dc63fa
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="getting-started-with-powershell-desired-state-configuration"></a><span data-ttu-id="712b2-103">Начало работы с настройкой требуемого состояния PowerShell</span><span class="sxs-lookup"><span data-stu-id="712b2-103">Getting Started with PowerShell Desired State Configuration</span></span> #

<span data-ttu-id="712b2-104">В этом руководстве описывается, как приступить к созданию документов настройки требуемого состояния PowerShell и применять их к компьютерам.</span><span class="sxs-lookup"><span data-stu-id="712b2-104">This guide describes how to begin creating PowerShell Desired State Configuration documents and apply them to machines.</span></span> <span data-ttu-id="712b2-105">Предполагается, что пользователь уже знаком с командлетами, модулями и компонентами PowerShell.</span><span class="sxs-lookup"><span data-stu-id="712b2-105">It assumes basic familiarity with PowerShell cmdlets, modules, and functions.</span></span>


## <a name="create-a-configuration"></a><span data-ttu-id="712b2-106">Создание конфигурации</span><span class="sxs-lookup"><span data-stu-id="712b2-106">Create a Configuration</span></span> ##

<span data-ttu-id="712b2-107">[**Конфигурации**](https://msdn.microsoft.com/powershell/dsc/configurations) — это документы, которые описывают среду.</span><span class="sxs-lookup"><span data-stu-id="712b2-107">[**Configurations**](https://msdn.microsoft.com/powershell/dsc/configurations) are documents that describe an environment.</span></span> <span data-ttu-id="712b2-108">Среды состоят из "**узлов**", которые обычно представляют собой компьютеры или виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="712b2-108">Environments consist of "**nodes**", which are commonly virtual or physical machines.</span></span>

<span data-ttu-id="712b2-109">Конфигурации могут иметь различные формы.</span><span class="sxs-lookup"><span data-stu-id="712b2-109">Configurations can come in a variety of forms.</span></span> <span data-ttu-id="712b2-110">Самый простой способ создания конфигурацию — с помощью PS1-файла (сценария PowerShell).</span><span class="sxs-lookup"><span data-stu-id="712b2-110">The easiest way to create a new configuration is to create a .ps1 (PowerShell script) file.</span></span> <span data-ttu-id="712b2-111">Чтобы создать этот файл, откройте любой текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="712b2-111">To do this, open your editor of choice.</span></span> <span data-ttu-id="712b2-112">Лучше всего использовать интегрированную среду сценариев PowerShell — она работает с DSC наилучшим образом.</span><span class="sxs-lookup"><span data-stu-id="712b2-112">The PowerShell ISE is a good choice, since it understands DSC natively.</span></span> <span data-ttu-id="712b2-113">Сохраните следующее как PS1-файл:</span><span class="sxs-lookup"><span data-stu-id="712b2-113">Save the following as a PS1:</span></span>

```powershell
configuration MyFirstConfiguration
{
    Import-DscResource -Name WindowsFeature

    Node localhost
    {
        WindowsFeature IIS
        {
            Name = "IIS"

        }

    }

}
```
## <a name="parts-of-a-configuration"></a><span data-ttu-id="712b2-114">Элементы конфигурации</span><span class="sxs-lookup"><span data-stu-id="712b2-114">Parts of a Configuration</span></span> ##
<span data-ttu-id="712b2-115">**Configuration** — это ключевое слово, добавленное в PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="712b2-115">**Configuration** is a keyword that has been added to PowerShell 4.0.</span></span> <span data-ttu-id="712b2-116">Оно означает особый вид компонентов PowerShell, используемых настройкой требуемого состояния.</span><span class="sxs-lookup"><span data-stu-id="712b2-116">It signifies a special kind of PowerShell function used by Desired State Configuration.</span></span> <span data-ttu-id="712b2-117">В этом примере компоненту присвоено имя myFirstConfiguration.</span><span class="sxs-lookup"><span data-stu-id="712b2-117">In this example, the function is named myFirstConfiguration.</span></span>

<span data-ttu-id="712b2-118">Следующая строка представляет собой оператор импорта, который аналогичен импорту модуля.</span><span class="sxs-lookup"><span data-stu-id="712b2-118">The next line is an import statement, similar to importing a module.</span></span> <span data-ttu-id="712b2-119">Его мы обсудим позже.</span><span class="sxs-lookup"><span data-stu-id="712b2-119">It will be discussed later on.</span></span>

<span data-ttu-id="712b2-120">Узел — это имя компьютера, на котором эта конфигурация будет запущена.</span><span class="sxs-lookup"><span data-stu-id="712b2-120">"Node" defines the machine name this configuration will act on.</span></span> <span data-ttu-id="712b2-121">Данная конфигурация редактируется локально, однако конфигурации могут охватывать не только локальные, но и удаленные узлы.</span><span class="sxs-lookup"><span data-stu-id="712b2-121">Although this configuration is edited locally, configurations can reach out to remote nodes and configure them.</span></span>

<span data-ttu-id="712b2-122">Узлы могут задаваться именами или IP-адресами компьютеров.</span><span class="sxs-lookup"><span data-stu-id="712b2-122">Nodes can be machine names or IP addresses.</span></span> <span data-ttu-id="712b2-123">Один документ конфигурации может содержать сразу несколько узлов.</span><span class="sxs-lookup"><span data-stu-id="712b2-123">You can have multiple nodes in a single configuration document.</span></span> <span data-ttu-id="712b2-124">Используя [данные конфигурации](https://msdn.microsoft.com/powershell/dsc/configdata), можно применить одну и ту же конфигурацию сразу к нескольким узлам.</span><span class="sxs-lookup"><span data-stu-id="712b2-124">Using [configuration data](https://msdn.microsoft.com/powershell/dsc/configdata), you can also have the same configuration apply to multiple nodes.</span></span> <span data-ttu-id="712b2-125">В данном случае указан узел localhost, т. е. локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="712b2-125">In this case, the node is "localhost" - which means the local computer.</span></span>

<span data-ttu-id="712b2-126">Следующий элемент — это [**ресурс**](https://msdn.microsoft.com/powershell/dsc/resources).</span><span class="sxs-lookup"><span data-stu-id="712b2-126">The next item is a [**resource**](https://msdn.microsoft.com/powershell/dsc/resources).</span></span> <span data-ttu-id="712b2-127">Ресурсы — это составные компоненты конфигураций.</span><span class="sxs-lookup"><span data-stu-id="712b2-127">Resources are building blocks of configurations.</span></span> <span data-ttu-id="712b2-128">Каждый ресурс — это модуль, определяющий логику реализации отдельного аспекта компьютера.</span><span class="sxs-lookup"><span data-stu-id="712b2-128">Each resource is a module that defines the implementation logic of a single aspect of a machine.</span></span> <span data-ttu-id="712b2-129">Каждый ресурс можно просмотреть на компьютере, выполнив командлет **Get-DscResource** в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="712b2-129">You can view every resource on your machine by running **Get-DscResource** in PowerShell.</span></span> <span data-ttu-id="712b2-130">Для использования в конфигурации ресурсы необходимо импортировать на локальный компьютер с помощью командлета **Import-DscResource**, который находится во второй строке данной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="712b2-130">Resources must be present on the local machine and imported before they can be used in a configuration with **Import-DscResource** which is on the second line of this configuration.</span></span>

<span data-ttu-id="712b2-131">**Активирование конфигурации**</span><span class="sxs-lookup"><span data-stu-id="712b2-131">**Enacting a Configuration**</span></span>

<span data-ttu-id="712b2-132">При сохранении и выполнении представленного выше сценария выходные данные не создаются.</span><span class="sxs-lookup"><span data-stu-id="712b2-132">If the script above is saved and run, no output will be produced.</span></span> <span data-ttu-id="712b2-133">Это связано с тем, что конфигурация — это просто функция, а в представленном выше сценарии эта функция определена, но еще не запущена.</span><span class="sxs-lookup"><span data-stu-id="712b2-133">This is because a configuration is just a function, and the script above has defined the function but not yet run it.</span></span> <span data-ttu-id="712b2-134">После определения функцию необходимо вызвать:</span><span class="sxs-lookup"><span data-stu-id="712b2-134">After the function is defined, it must be invoked:</span></span>
```powershell
myFirstConfiguration
```

<span data-ttu-id="712b2-135">Во время выполнения функции конфигурации проверяют ее работоспособность.</span><span class="sxs-lookup"><span data-stu-id="712b2-135">When executed, configuration functions validate the configuration is valid.</span></span> <span data-ttu-id="712b2-136">В конфигурации не должно быть синтаксических ошибок, в ресурсах должны присутствовать все обязательные параметры, при этом все ресурсы перед выполнением должны быть импортированы.</span><span class="sxs-lookup"><span data-stu-id="712b2-136">It should have no syntax errors, resources should have all mandatory parameters defined, and all resources should be imported before execution.</span></span>

<span data-ttu-id="712b2-137">После выполнения конфигурации создается папка с именем конфигурации, содержащая **MOF-файл** для каждого включенного в нее узла.</span><span class="sxs-lookup"><span data-stu-id="712b2-137">Once the configuration is executed, it creates a folder with the name of the configuration containing a **.MOF file** for every node in the configuration.</span></span> <span data-ttu-id="712b2-138">MOF-файл — это формат управления на основе стандартов, используемый DSC PowerShell для обмена данными по сети.</span><span class="sxs-lookup"><span data-stu-id="712b2-138">The .MOF file is a standards-based management format which is used by PowerShell DSC to communicate over the network.</span></span>

<span data-ttu-id="712b2-139">Активирование конфигурации:</span><span class="sxs-lookup"><span data-stu-id="712b2-139">To enact the configuration:</span></span>
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration
```
<span data-ttu-id="712b2-140">Эта команда создает задание PowerShell, которое настраивает указанные в конфигурации узлы.</span><span class="sxs-lookup"><span data-stu-id="712b2-140">This creates a PowerShell job that reaches out to the nodes in the configuration and configures them.</span></span> <span data-ttu-id="712b2-141">Для просмотра выходных данных задания используйте параметр -Wait.</span><span class="sxs-lookup"><span data-stu-id="712b2-141">To see the output of the job, use -Wait.</span></span>
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration -Wait
```