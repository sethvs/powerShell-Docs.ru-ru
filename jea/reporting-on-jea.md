---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "отчеты о jea"
ms.technology: powershell
ms.openlocfilehash: 3e7bd2755281f491bba8a905df018fb2e1cac6ff
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
# <a name="reporting-on-jea"></a><span data-ttu-id="ab384-103">Отчеты о JEA</span><span class="sxs-lookup"><span data-stu-id="ab384-103">Reporting on JEA</span></span>
<span data-ttu-id="ab384-104">Так как JEA позволяет непривилегированным пользователям работать в привилегированном контексте, ведение журнала и аудит получают особое значение.</span><span class="sxs-lookup"><span data-stu-id="ab384-104">Because JEA allows non-privileged users to run in a privileged context, logging and auditing are extremely important.</span></span>
<span data-ttu-id="ab384-105">В этом разделе мы рассмотрим инструменты, которые помогут вам вести журналы и отчетность.</span><span class="sxs-lookup"><span data-stu-id="ab384-105">In this section, we'll run through the tools you can use to help you with logging and reporting.</span></span>

## <a name="reporting-on-jea-actions"></a><span data-ttu-id="ab384-106">Отчеты о действиях JEA</span><span class="sxs-lookup"><span data-stu-id="ab384-106">Reporting on JEA Actions</span></span>
### <a name="over-the-shoulder-transcription"></a><span data-ttu-id="ab384-107">Запись с "подсматриванием"</span><span class="sxs-lookup"><span data-stu-id="ab384-107">Over-the-Shoulder Transcription</span></span>
<span data-ttu-id="ab384-108">Один из самых быстрых способов понять, что происходит в сеансе PowerShell, — просто подсмотреть за пользователем.</span><span class="sxs-lookup"><span data-stu-id="ab384-108">One of the quickest ways to get a summary of what's happening in a PowerShell session is to look over the shoulder of the person typing.</span></span>
<span data-ttu-id="ab384-109">Вы увидите команды, результаты выполнения этих команд и убедитесь, что все в порядке.</span><span class="sxs-lookup"><span data-stu-id="ab384-109">You see their commands, the output of those commands, and all is well.</span></span>
<span data-ttu-id="ab384-110">Если что-то не так, вы по меньшей мере об этом узнаете.</span><span class="sxs-lookup"><span data-stu-id="ab384-110">Or it's not, but at least you'll know.</span></span>
<span data-ttu-id="ab384-111">Запись PowerShell позволяет получить похожее представление постфактум.</span><span class="sxs-lookup"><span data-stu-id="ab384-111">PowerShell transcription is designed to give you a similar view after the fact.</span></span>

<span data-ttu-id="ab384-112">При использовании поля "TranscriptDirectory" в конфигурации сеанса PowerShell автоматически запишет все действия пользователя, предпринятые в течение данного сеанса.</span><span class="sxs-lookup"><span data-stu-id="ab384-112">When using the "TranscriptDirectory" field in your Session Configuration, PowerShell will automatically record a transcript of all actions taken in a given session.</span></span>
<span data-ttu-id="ab384-113">Записи сеансов см. в документе, который находится в папке "$env:ProgramData\JEAConfiguration\Transcripts".</span><span class="sxs-lookup"><span data-stu-id="ab384-113">You can find transcripts from your sessions in this document here: "$env:ProgramData\JEAConfiguration\Transcripts"</span></span>

<span data-ttu-id="ab384-114">Как можно видеть, запись содержит сведения о подключенном пользователе, пользователе, от имени которого ведется работа, выполняемые в ходе сеанса команды и многое другое.</span><span class="sxs-lookup"><span data-stu-id="ab384-114">As you can tell, the transcript records information about the "Connected" user, the "Run As" user, the commands run in the session, and more.</span></span>
<span data-ttu-id="ab384-115">Дополнительные сведения о записях PowerShell см. в этой [записи в блоге](http://blogs.msdn.com/b/powershell/archive/2015/06/09/powershell-the-blue-team.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab384-115">For more information about PowerShell transcription, check out [this blog post](http://blogs.msdn.com/b/powershell/archive/2015/06/09/powershell-the-blue-team.aspx).</span></span>

### <a name="powershell-event-logs"></a><span data-ttu-id="ab384-116">Журналы событий PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab384-116">PowerShell Event Logs</span></span>
<span data-ttu-id="ab384-117">После того как вы включите запись журнала модуля, все действия PowerShell будут также записываться в обычные журналы событий Windows.</span><span class="sxs-lookup"><span data-stu-id="ab384-117">When you have module logging turned on, all PowerShell actions are also recorded in regular Windows Event logs.</span></span>
<span data-ttu-id="ab384-118">Работать с ними сложнее, чем с записями, но журналы обеспечивают более глубокий уровень детализации.</span><span class="sxs-lookup"><span data-stu-id="ab384-118">This is slightly messier to deal with when compared to transcripts, but the level of detail it gives you can be useful.</span></span>

<span data-ttu-id="ab384-119">Если ведение журнала модулей включено, по идентификатору события 4104 в журнале операций PowerShell можно видеть запись всех вызванных команд.</span><span class="sxs-lookup"><span data-stu-id="ab384-119">In the "PowerShell" operational log, Event ID 4104 will record each command invoked if you have enabled module logging.</span></span>

### <a name="other-event-logs"></a><span data-ttu-id="ab384-120">Другие журналы событий</span><span class="sxs-lookup"><span data-stu-id="ab384-120">Other Event Logs</span></span>
<span data-ttu-id="ab384-121">В отличие от журналов и записей PowerShell, другие механизмы ведения журнала не записывают действия подключенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="ab384-121">Unlike PowerShell logs and transcripts, other logging mechanisms will not capture the "Connected User".</span></span>
<span data-ttu-id="ab384-122">Для сопоставления предпринятых действий потребуется соотнести журналы PowerShell и другие журналы.</span><span class="sxs-lookup"><span data-stu-id="ab384-122">You will need to do some correlation between other logs and PowerShell logs to match up actions taken.</span></span>

<span data-ttu-id="ab384-123">По идентификатору события 193 в журнале операций "Служба удаленного управления Windows" будут записаны SID и имя подключенного пользователя, а также SID виртуальной учетной записи запуска от имени для подобного соотнесения.</span><span class="sxs-lookup"><span data-stu-id="ab384-123">In the "Windows Remote Management" operational log, Event ID 193 will record the Connecting User's SID and Name, as well as the RunAs Virtual Account's SID to assist with this correlation.</span></span>
<span data-ttu-id="ab384-124">Как вы могли заметить, имя виртуальной учетной записи запуска от имени заканчивается именем домена и именем подключенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="ab384-124">You may have also noticed that the name of the RunAs Virtual Account includes the connecting user's domain and username at the end.</span></span>

## <a name="reporting-on-jea-configuration"></a><span data-ttu-id="ab384-125">Отчеты о конфигурации JEA</span><span class="sxs-lookup"><span data-stu-id="ab384-125">Reporting on JEA Configuration</span></span>
### <a name="get-pssessionconfiguration"></a><span data-ttu-id="ab384-126">Get-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="ab384-126">Get-PSSessionConfiguration</span></span>
<span data-ttu-id="ab384-127">Для получения точных отчетов о состоянии среды важно знать, сколько конечных точек JEA настроено на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ab384-127">In order to accurately report on the state of your environment, it's important to know how many JEA endpoints you have set up on your machine.</span></span>
<span data-ttu-id="ab384-128">`Get-PSSessionConfiguration` делает именно это.</span><span class="sxs-lookup"><span data-stu-id="ab384-128">`Get-PSSessionConfiguration` does just that.</span></span>

### <a name="get-pssessioncapability"></a><span data-ttu-id="ab384-129">Get-PSSessionCapability</span><span class="sxs-lookup"><span data-stu-id="ab384-129">Get-PSSessionCapability</span></span>
<span data-ttu-id="ab384-130">Создавать отчеты по возможностям того или иного пользователя через конечную точку JEA может быть непросто.</span><span class="sxs-lookup"><span data-stu-id="ab384-130">Manually reporting on the capabilities of any given user through a JEA endpoint can be quite complex.</span></span>
<span data-ttu-id="ab384-131">Для этого иногда придется проверить несколько отдельных возможностей ролей.</span><span class="sxs-lookup"><span data-stu-id="ab384-131">You would potentially need to inspect several role capabilities.</span></span>
<span data-ttu-id="ab384-132">К счастью, с этой задачей справляется командлет "Get-PSSessionCapability".</span><span class="sxs-lookup"><span data-stu-id="ab384-132">Fortunately, the "Get-PSSessionCapability" cmdlet does this.</span></span>

<span data-ttu-id="ab384-133">Чтобы убедиться, выполните следующую команду в командной строке администратора PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ab384-133">To test this out, run the following command from an administrator PowerShell prompt:</span></span>
```PowerShell
Get-PSSessionCapability -Username 'CONTOSO\OperatorUser' -ConfigurationName JEADemo
```

