---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс nxGroup в DSC для Linux"
ms.openlocfilehash: fcd1dfd3110b1358ed7ef9ca8d57154186b271f6
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-for-linux-nxgroup-resource"></a><span data-ttu-id="e12ae-103">Ресурс nxGroup в DSC для Linux</span><span class="sxs-lookup"><span data-stu-id="e12ae-103">DSC for Linux nxGroup Resource</span></span>

<span data-ttu-id="e12ae-104">Ресурс **nxGroup** в DSC PowerShell предоставляет механизм управления локальными группами на узле Linux.</span><span class="sxs-lookup"><span data-stu-id="e12ae-104">The **nxGroup** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="e12ae-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="e12ae-105">Syntax</span></span>

```powershell
nxGroup <string> #ResourceName
{
    GroupName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Members = <string[]> ]
    [ MebersToInclude = <string[]>]
    [ MembersToExclude = <string[]> ]
    [ DependsOn = <string[]> ]
}

```

## <a name="properties"></a><span data-ttu-id="e12ae-106">Свойства</span><span class="sxs-lookup"><span data-stu-id="e12ae-106">Properties</span></span>

|  <span data-ttu-id="e12ae-107">Свойство</span><span class="sxs-lookup"><span data-stu-id="e12ae-107">Property</span></span> |  <span data-ttu-id="e12ae-108">Описание</span><span class="sxs-lookup"><span data-stu-id="e12ae-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="e12ae-109">GroupName</span><span class="sxs-lookup"><span data-stu-id="e12ae-109">GroupName</span></span>| <span data-ttu-id="e12ae-110">Указывает имя группы, для которой требуется обеспечить определенное состояние.</span><span class="sxs-lookup"><span data-stu-id="e12ae-110">Specifies the name of the group for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="e12ae-111">Ensure</span><span class="sxs-lookup"><span data-stu-id="e12ae-111">Ensure</span></span>| <span data-ttu-id="e12ae-112">Определяет, нужно ли проверять существование группы.</span><span class="sxs-lookup"><span data-stu-id="e12ae-112">Determines whether to check if the group exists.</span></span> <span data-ttu-id="e12ae-113">Чтобы убедиться, что группа существует, укажите для этого свойства значение Present.</span><span class="sxs-lookup"><span data-stu-id="e12ae-113">Set this property to "Present" to ensure the group exists.</span></span> <span data-ttu-id="e12ae-114">Чтобы убедиться, что группа не существует, укажите для этого свойства значение Absent.</span><span class="sxs-lookup"><span data-stu-id="e12ae-114">Set it to "Absent" to ensure the group does not exist.</span></span> <span data-ttu-id="e12ae-115">Значение по умолчанию — Present.</span><span class="sxs-lookup"><span data-stu-id="e12ae-115">The default value is "Present".</span></span>| 
| <span data-ttu-id="e12ae-116">Члены группы</span><span class="sxs-lookup"><span data-stu-id="e12ae-116">Members</span></span>| <span data-ttu-id="e12ae-117">Указывает членов группы.</span><span class="sxs-lookup"><span data-stu-id="e12ae-117">Specifies the members that form the group.</span></span>| 
| <span data-ttu-id="e12ae-118">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="e12ae-118">MembersToInclude</span></span>| <span data-ttu-id="e12ae-119">Указывает пользователей, которых нужно добавить в группу.</span><span class="sxs-lookup"><span data-stu-id="e12ae-119">Specifies the users who you want to ensure are members of the group.</span></span>| 
| <span data-ttu-id="e12ae-120">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="e12ae-120">MembersToExclude</span></span>| <span data-ttu-id="e12ae-121">Указывает пользователей, которых нужно исключить из группы.</span><span class="sxs-lookup"><span data-stu-id="e12ae-121">Specifies the users who you want to ensure are not members of the group.</span></span>| 
| <span data-ttu-id="e12ae-122">PreferredGroupID</span><span class="sxs-lookup"><span data-stu-id="e12ae-122">PreferredGroupID</span></span>| <span data-ttu-id="e12ae-123">По возможности задает в качестве идентификатора группы указанное значение.</span><span class="sxs-lookup"><span data-stu-id="e12ae-123">Sets the group id to the provided value if possible.</span></span> <span data-ttu-id="e12ae-124">Если этот идентификатор группы сейчас используется, выбирается следующий доступный идентификатор группы.</span><span class="sxs-lookup"><span data-stu-id="e12ae-124">If the group id is currently in use, the next available group id is used.</span></span>| 
| <span data-ttu-id="e12ae-125">DependsOn</span><span class="sxs-lookup"><span data-stu-id="e12ae-125">DependsOn</span></span> | <span data-ttu-id="e12ae-126">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="e12ae-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="e12ae-127">Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="e12ae-127">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="example"></a><span data-ttu-id="e12ae-128">Пример</span><span class="sxs-lookup"><span data-stu-id="e12ae-128">Example</span></span>

<span data-ttu-id="e12ae-129">В следующем примере удостоверяется, что пользователь monuser существует и является членом группы DBusers.</span><span class="sxs-lookup"><span data-stu-id="e12ae-129">The following example ensures that the user “monuser” exists and is a member of the group "DBusers".</span></span>

```
Import-DSCResource -Module nx 

Node $node {

nxUser UserExample{
   UserName = "monuser"
   Description = "Monitoring user"
   Password  =    '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
   Ensure = "Present"
   HomeDirectory = "/home/monuser"
}
 
nxGroup GroupExample{
   GroupName = "DBusers"
   Ensure = "Present"
   MembersToInclude = "monuser"
   DependsOn = "[nxUser]UserExample"            
}
}
```

