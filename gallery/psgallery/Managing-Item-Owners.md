---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "коллекции,powershell,командлет,psgallery"
title: "Управление владельцами элементов"
ms.openlocfilehash: fcd538148f9ff1ac96324b567d54d643f1756c93
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="managing-item-owners"></a><span data-ttu-id="86957-103">Управление владельцами элементов</span><span class="sxs-lookup"><span data-stu-id="86957-103">Managing Item Owners</span></span>

<span data-ttu-id="86957-104">Владелец элемента в коллекции PowerShell определяется по тому, кто опубликовал элемент в коллекции.</span><span class="sxs-lookup"><span data-stu-id="86957-104">Ownership of an item in the PowerShell Gallery is defined by who published the item to the gallery.</span></span>
<span data-ttu-id="86957-105">Иногда этими метаданными необходимо управлять после первоначальной публикации элементов, а значит владелец метаданных должен быть изменяемым, даже если сам элемент таковым не является.</span><span class="sxs-lookup"><span data-stu-id="86957-105">Sometimes this metadata needs to be managed beyond the initial item publishing, which means the owner metadata needs to be mutable while the item itself is not.</span></span>

<span data-ttu-id="86957-106">Все владельцы элементов равноправны.</span><span class="sxs-lookup"><span data-stu-id="86957-106">All item owners are peers.</span></span> <span data-ttu-id="86957-107">Это значит, что любой владелец элемента может опубликовать его новую версию.</span><span class="sxs-lookup"><span data-stu-id="86957-107">This means any item owner can publish a new version of an item.</span></span> <span data-ttu-id="86957-108">Это также означает, что любой владелец элемента может удалить любого другого владельца этого элемента.</span><span class="sxs-lookup"><span data-stu-id="86957-108">It also means that any item owner can remove any other item owner.</span></span> <span data-ttu-id="86957-109">Ни один владелец не имеет больше полномочий, чем другие.</span><span class="sxs-lookup"><span data-stu-id="86957-109">No owner has more authority than other owners.</span></span>  

## <a name="setting-an-items-initial-owner"></a><span data-ttu-id="86957-110">Настройка первоначального владельца элемента</span><span class="sxs-lookup"><span data-stu-id="86957-110">Setting an Item's Initial Owner</span></span> 

<span data-ttu-id="86957-111">При публикации элемента в коллекции PowerShell первоначального владельца определяет пользователь, публикующий этот элемент.</span><span class="sxs-lookup"><span data-stu-id="86957-111">When a new item is published to PowerShell Gallery, the initial owner is defined by the user that published the item.</span></span> <span data-ttu-id="86957-112">Он определяется по ключу интерфейса API, который использовался в командлете Publish-Module.</span><span class="sxs-lookup"><span data-stu-id="86957-112">This is determined by whose API key was used in the Publish-Module cmdlet.</span></span>

## <a name="adding-owners"></a><span data-ttu-id="86957-113">Добавление владельцев</span><span class="sxs-lookup"><span data-stu-id="86957-113">Adding Owners</span></span>

<span data-ttu-id="86957-114">После публикации элемента в коллекции PowerShell можно пригласить стать его владельцами дополнительных пользователей.</span><span class="sxs-lookup"><span data-stu-id="86957-114">Once an item has been published to the PowerShell Gallery, it's easy to invite additional users to become owners of an item.</span></span>

1. <span data-ttu-id="86957-115">[Войдите](https://powershellgallery.com/users/account/LogOn) в коллекцию PowerShell по учетной записи текущего владельца элемента.</span><span class="sxs-lookup"><span data-stu-id="86957-115">[Log on](https://powershellgallery.com/users/account/LogOn) to the PowerShell Gallery with the account that is the current owner of an item.</span></span>
2. <span data-ttu-id="86957-116">Перейдите на страницу элемента, открыв вкладку "Элементы", выполнив поиск или щелкнув свое имя пользователя, и выберите пункт [**Управление моими элементами**](https://www.powershellgallery.com/account/Packages).</span><span class="sxs-lookup"><span data-stu-id="86957-116">Navigate to an item page using the 'Items' tab, searching, or clicking your username and then [**Manage My Items**](https://www.powershellgallery.com/account/Packages).</span></span>
3. <span data-ttu-id="86957-117">Выполнив вход в систему как владелец элемента, щелкните слева ссылку "Управление владельцами".</span><span class="sxs-lookup"><span data-stu-id="86957-117">When logged on as an item's owner, there is a 'Manage Owners' link on the left side to click.</span></span>
4. <span data-ttu-id="86957-118">Введите имя пользователя, которого нужно добавить в качестве владельца, и нажмите кнопку "Добавить".</span><span class="sxs-lookup"><span data-stu-id="86957-118">Enter the username of the person to add as an owner and click 'Add'.</span></span>
5. <span data-ttu-id="86957-119">После этого новому совладельцу будет отправлено электронное письмо с приглашением стать владельцем элемента.</span><span class="sxs-lookup"><span data-stu-id="86957-119">An email is then sent to the new co-owner, as an invitation to become an owner of an item.</span></span>
6. <span data-ttu-id="86957-120">Щелкнув ссылку в этом письме, пользователь станет совладельцем элемента со всеми правами и, в том числе, сможет удалить других пользователей из числа владельцев.</span><span class="sxs-lookup"><span data-stu-id="86957-120">Once that user clicks the link, they are a full co-owner with full control over an item, including the ability to remove other users as owners.</span></span>

<span data-ttu-id="86957-121">**ПРИМЕЧАНИЕ**. Пока новый пользователь не подтвердит владение, он *не будет* числиться владельцем элемента.</span><span class="sxs-lookup"><span data-stu-id="86957-121">**NOTE**: Until the new owner confirms ownership, they *will not* be listed as an owner of an item.</span></span>
<span data-ttu-id="86957-122">В списке текущих владельцев на странице **Управление владельцами** для него будет отображаться запись "Ожидает подтверждения".</span><span class="sxs-lookup"><span data-stu-id="86957-122">When viewing the **Manage Owners** page, you will see a "pending approval" entry in the current owners.</span></span>
<span data-ttu-id="86957-123">Приглашение, как и других владельцев, можно удалить.</span><span class="sxs-lookup"><span data-stu-id="86957-123">That invitation can be removed; just as other owners can be removed.</span></span>
<span data-ttu-id="86957-124">Процедура приглашения защищает пользователей от ошибочного добавления других пользователей в число владельцев элемента.</span><span class="sxs-lookup"><span data-stu-id="86957-124">This process of invitations prevents users from falsely adding other users as owners of their items.</span></span>

<span data-ttu-id="86957-125">Обратите внимание, что метаданные "Авторы" заполняются произвольно, контролируются только "Владельцы".</span><span class="sxs-lookup"><span data-stu-id="86957-125">Note that the "Authors" metadata is purely freeform text; only "Owners" are controlled.</span></span>


## <a name="removing-owners"></a><span data-ttu-id="86957-126">Удаление владельцев</span><span class="sxs-lookup"><span data-stu-id="86957-126">Removing Owners</span></span>
<span data-ttu-id="86957-127">Если элемент имеет несколько владельцев и одного из них нужно удалить, это делается очень просто:</span><span class="sxs-lookup"><span data-stu-id="86957-127">When an item has multiple owners and one needs to be removed, the process is simple:</span></span>

1. <span data-ttu-id="86957-128">[Войдите](https://powershellgallery.com/users/account/LogOn) в коллекцию PowerShell по учетной записи текущего владельца элемента.</span><span class="sxs-lookup"><span data-stu-id="86957-128">[Log on](https://powershellgallery.com/users/account/LogOn) to PowerShell Gallery with the account that is the current owner of an item;</span></span>
2. <span data-ttu-id="86957-129">Перейдите на страницу элемента, открыв вкладку "Элементы", выполнив поиск или щелкнув свое имя пользователя, и выберите пункт [**Управление моими элементами**](https://www.powershellgallery.com/account/Packages).</span><span class="sxs-lookup"><span data-stu-id="86957-129">Navigate to an item page using the Items tab, searching, or clicking your username and then [**Manage My Items**](https://www.powershellgallery.com/account/Packages).</span></span>
3. <span data-ttu-id="86957-130">Выполнив вход в систему как владелец элемента, щелкните слева ссылку "Управление владельцами".</span><span class="sxs-lookup"><span data-stu-id="86957-130">When logged on as an item's owner, there is a 'Manage Owners' link on the left side to click;</span></span>
4. <span data-ttu-id="86957-131">Щелкните ссылку "Удалить" рядом с удаляемым владельцем.</span><span class="sxs-lookup"><span data-stu-id="86957-131">Click the 'remove' link next to the owner to be removed.</span></span>



## <a name="transferring-item-ownership"></a><span data-ttu-id="86957-132">Передача владения элементом</span><span class="sxs-lookup"><span data-stu-id="86957-132">Transferring Item Ownership</span></span>
<span data-ttu-id="86957-133">Иногда мы получаем запросы о передаче владения элементом от одного пользователя другому, но почти всегда вы можете сделать это сами.</span><span class="sxs-lookup"><span data-stu-id="86957-133">We sometimes get support requests to transfer item ownership from one user to another, but you can almost always accomplish this yourself.</span></span>
<span data-ttu-id="86957-134">Передача владения от одного пользователя другому представляет собой простую комбинацию двух описанных выше функций.</span><span class="sxs-lookup"><span data-stu-id="86957-134">Transferring ownership from one user to another is simply a combination of the two features above.</span></span>

1. <span data-ttu-id="86957-135">Текущий владелец приглашает нового пользователя в качестве совладельца, а новый пользователь принимает приглашение.</span><span class="sxs-lookup"><span data-stu-id="86957-135">The current owner invites the new user to become a co-owner and the new user accepts the invite;</span></span>
2. <span data-ttu-id="86957-136">Новый пользователь удаляет старого пользователя из списка владельцев.</span><span class="sxs-lookup"><span data-stu-id="86957-136">The new user removes the old user from the list of owners.</span></span>

<span data-ttu-id="86957-137">Это действие может потребоваться по ряду причин, но процедура всегда одна и та же.</span><span class="sxs-lookup"><span data-stu-id="86957-137">This request has come in under a couple forms but the process works the same.</span></span>

* <span data-ttu-id="86957-138">Владельцем элемента вместо одного разработчика становится другой.</span><span class="sxs-lookup"><span data-stu-id="86957-138">The item ownership is changing from one developer to another</span></span>
* <span data-ttu-id="86957-139">Элемент был случайно опубликован не под той учетной записью.</span><span class="sxs-lookup"><span data-stu-id="86957-139">The item was accidentally published using the wrong account</span></span>


## <a name="orphaned-items"></a><span data-ttu-id="86957-140">Потерянные элементы</span><span class="sxs-lookup"><span data-stu-id="86957-140">Orphaned Items</span></span>
<span data-ttu-id="86957-141">Возможна и еще одна ситуация, но встречается она нечасто.</span><span class="sxs-lookup"><span data-stu-id="86957-141">One last scenario has occurred, but not many times.</span></span>
<span data-ttu-id="86957-142">Элементы теряются (учетная запись единственного владельца не может быть использована, чтобы добавить новых владельцев).</span><span class="sxs-lookup"><span data-stu-id="86957-142">Items have become orphans and the only item owner account cannot be used to add new owners.</span></span>
<span data-ttu-id="86957-143">Приведем несколько примеров такой ситуации.</span><span class="sxs-lookup"><span data-stu-id="86957-143">Here are some examples of this scenario:</span></span>

* <span data-ttu-id="86957-144">Учетная запись владельца связана с адресом электронной почты, который больше не существует, либо пользователь забыл пароль.</span><span class="sxs-lookup"><span data-stu-id="86957-144">The owner's account is associated with an email address that no longer exists and the user has forgotten their password</span></span>
* <span data-ttu-id="86957-145">Зарегистрированный владелец уволился из компании, в которой был создан элемент, и связаться с ним для того, чтобы изменить владельца этого элемента, не удается.</span><span class="sxs-lookup"><span data-stu-id="86957-145">The registered owner has left the company that produces the item and cannot be reached to update the item ownership</span></span>
* <span data-ttu-id="86957-146">Из-за ошибки, которая затронула лишь небольшое число элементов, элемент остался без владельца.</span><span class="sxs-lookup"><span data-stu-id="86957-146">Due to a bug that has only affected a handful of items, the item is somehow ownerless on the gallery</span></span>

<span data-ttu-id="86957-147">Администраторы коллекции PowerShell имеют доступ к ссылке "Управление владельцами" любого элемента.</span><span class="sxs-lookup"><span data-stu-id="86957-147">The PowerShell Gallery Administrators can access the 'Manage Owners' link for any item.</span></span>
<span data-ttu-id="86957-148">Если вы являетесь действительным владельцем элемента и не можете связаться с текущим владельцем, чтобы получить разрешения на владение, щелкните ссылку "Сообщить о нарушении" в коллекции, чтобы связаться с администраторами коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86957-148">If you are the rightful owner of a item and cannot reach the current owner to gain ownership permissions, then use the 'Report Abuse' link on the gallery to reach the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="86957-149">Мы выполним процедуру проверки, чтобы подтвердить, что вы действительно имеете право владеть элементом.</span><span class="sxs-lookup"><span data-stu-id="86957-149">We will then follow a process to verify your ownership of the item.</span></span>
<span data-ttu-id="86957-150">Если мы определим, что владельцем элемента должны быть вы, мы сами воспользуемся ссылкой "Управление владельцами" и отправим вам приглашение стать владельцем.</span><span class="sxs-lookup"><span data-stu-id="86957-150">If we determine you should be an owner of the item, we will use the 'Manage Owners' link for the item ourselves and send you the invite to become an owner.</span></span>
<span data-ttu-id="86957-151">Мы сделаем это только после того, как убедимся, что вы должны быть владельцем; дальнейший порядок действий зависит от ситуации.</span><span class="sxs-lookup"><span data-stu-id="86957-151">We will only do this after verifying that you should be an owner and the process for this varies by circumstances.</span></span>
<span data-ttu-id="86957-152">Во многих случаях мы попытаемся связаться с владельцем проекта, используя проектный URL-адрес элемента, но можем связаться с ним также через Twitter, по электронной почте или другими способами.</span><span class="sxs-lookup"><span data-stu-id="86957-152">Often times, we will use the item's Project URL to find a way to contact the project owner, but we may also use Twitter, Email, or other means for contacting the project owner.</span></span>

