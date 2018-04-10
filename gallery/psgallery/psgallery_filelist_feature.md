---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: коллекции,powershell,командлет,psgallery
title: psgallery_функция_filelist
ms.openlocfilehash: 92dd22aaf9a1ce3ac40372ffc11d26d8c3e79dd1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="filelist-feature-in-the-gallery"></a><span data-ttu-id="15acc-103">Функция FileList в коллекции</span><span class="sxs-lookup"><span data-stu-id="15acc-103">FileList Feature in the Gallery</span></span>

<span data-ttu-id="15acc-104">Вы можете просматривать содержимое всех элементов, опубликованных в коллекции.</span><span class="sxs-lookup"><span data-stu-id="15acc-104">You are able to view the contents in all items published in the gallery.</span></span>

<span data-ttu-id="15acc-105">Эта функция состоит из двух частей: отображение списка файлов элемента и содержимого поддерживаемых типов файлов.</span><span class="sxs-lookup"><span data-stu-id="15acc-105">This feature includes two parts: listing the files within the item, and displaying file contents for supported file types.</span></span> <span data-ttu-id="15acc-106">В настоящее время поддерживается отображение содержимого файлов со следующими расширениями: PS1, PSM1, PSD1, PS1XML, XML и TXT.</span><span class="sxs-lookup"><span data-stu-id="15acc-106">Currently we support displaying the contents of the following file extensions: .ps1, .psm1, .psd1, .ps1xml, .xml and .txt.</span></span> <span data-ttu-id="15acc-107">В следующих версиях будет добавлена поддержка дополнительных расширений.</span><span class="sxs-lookup"><span data-stu-id="15acc-107">We will be supporting more file extensions in the next releases.</span></span>

## <a name="where-to-find-filelist"></a><span data-ttu-id="15acc-108">Где находится FileList</span><span class="sxs-lookup"><span data-stu-id="15acc-108">Where to Find FileList</span></span>
<span data-ttu-id="15acc-109">На странице каждого отдельного элемента имеется раздел FileList и ссылка **Показать**.</span><span class="sxs-lookup"><span data-stu-id="15acc-109">On each individual item page, you will be able to find FileList section and a **Show** link.</span></span> <span data-ttu-id="15acc-110">Щелкните ссылку "Показать". Откроется полный список элементов, содержащихся в элементе.</span><span class="sxs-lookup"><span data-stu-id="15acc-110">Click on the Show and you will find a complete list of items contained in the item.</span></span>

<span data-ttu-id="15acc-111">Каждый поддерживаемый тип файлов отображается как гиперссылка, щелкнув которую вы перейдете на новую страницу, где содержимое файла будет показано с выделением синтаксиса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15acc-111">Each supported file type is displayed as a hyperlink, and clicking it will take you to a new page with file contents displayed in PowerShell syntax highlighting.</span></span> <span data-ttu-id="15acc-112">Щелкнув заголовок или версию элемента, отображаемые в верхней части экрана, вы вернетесь на страницу подробностей об элементе.</span><span class="sxs-lookup"><span data-stu-id="15acc-112">Clicking on the title or the version of the item, which is displayed at the top of the screen, will bring you back to item detail page.</span></span>