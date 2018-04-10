---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 62cccabd7c63c6ba928fc2bf8addd3d11483e90f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="get-childitem-has--depth-parameter"></a><span data-ttu-id="f7ee2-102">Get-ChildItem получает параметр -Depth</span><span class="sxs-lookup"><span data-stu-id="f7ee2-102">Get-ChildItem has -Depth parameter</span></span>
<span data-ttu-id="f7ee2-103">Теперь **Get-ChildItem** имеет параметр **Depth**, используемый вместе с **–Recurse** для ограничения рекурсии:</span><span class="sxs-lookup"><span data-stu-id="f7ee2-103">**Get-ChildItem** now has a **–Depth** parameter you use with **–Recurse** to limit the recursion:</span></span>

<span data-ttu-id="f7ee2-104">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 0</span><span class="sxs-lookup"><span data-stu-id="f7ee2-104">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 0</span></span>

<span data-ttu-id="f7ee2-105">Каталог: C:\\Users\\slee\\Downloads\\Example</span><span class="sxs-lookup"><span data-stu-id="f7ee2-105">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="f7ee2-106">Mode LastWriteTime Length Name</span><span class="sxs-lookup"><span data-stu-id="f7ee2-106">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="f7ee2-107">d----- 4/14/2015 5:36 PM Depth0</span><span class="sxs-lookup"><span data-stu-id="f7ee2-107">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="f7ee2-108">-a---- 4/14/2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="f7ee2-108">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="f7ee2-109">-a---- 4/14/2015 1:19 PM 0 File2.txt</span><span class="sxs-lookup"><span data-stu-id="f7ee2-109">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="f7ee2-110">-a---- 4/14/2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="f7ee2-110">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="f7ee2-111">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 1</span><span class="sxs-lookup"><span data-stu-id="f7ee2-111">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 1</span></span>

<span data-ttu-id="f7ee2-112">Каталог: C:\\Users\\slee\\Downloads\\Example</span><span class="sxs-lookup"><span data-stu-id="f7ee2-112">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="f7ee2-113">Mode LastWriteTime Length Name</span><span class="sxs-lookup"><span data-stu-id="f7ee2-113">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="f7ee2-114">d----- 4/14/2015 5:36 PM Depth0</span><span class="sxs-lookup"><span data-stu-id="f7ee2-114">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="f7ee2-115">-a---- 4/14/2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="f7ee2-115">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="f7ee2-116">-a---- 4/14/2015 1:19 PM 0 File2.txt</span><span class="sxs-lookup"><span data-stu-id="f7ee2-116">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="f7ee2-117">-a---- 4/14/2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="f7ee2-117">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="f7ee2-118">Каталог: C:\\Users\\slee\\Downloads\\Example\\Depth0</span><span class="sxs-lookup"><span data-stu-id="f7ee2-118">Directory: C:\\Users\\slee\\Downloads\\Example\\Depth0</span></span>

<span data-ttu-id="f7ee2-119">Mode LastWriteTime Length Name</span><span class="sxs-lookup"><span data-stu-id="f7ee2-119">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="f7ee2-120">d----- 4/14/2015 5:33 PM Depth1</span><span class="sxs-lookup"><span data-stu-id="f7ee2-120">d----- 4/14/2015 5:33 PM Depth1</span></span>