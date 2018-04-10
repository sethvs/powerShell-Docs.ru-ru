---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Функция DSC для запроса сведений об узле с опрашивающего сервера.
ms.openlocfilehash: 5c10eefe9ded4fe6339c4e6252cc189bcd793978
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-function-to-query-node-information-from-pull-server"></a>Функция DSC для запроса сведений об узле с опрашивающего сервера.

```powershell
function QueryNodeInformation
{
Param (
       [string] $Uri =
"http://localhost:7070/PSDSCComplianceServer.svc/Status",
       [string] $ContentType = "application/json"
     )

  Write-Host "Querying node information from pull server URI  = $Uri" -ForegroundColor Green

  Write-Host "Querying node status in content type  = $ContentType " -ForegroundColor Green

   $response = Invoke-WebRequest -Uri $Uri -Method Get -ContentType $ContentType -UseDefaultCredentials -Headers
    @{Accept = $ContentType}

   if($response.StatusCode -ne 200)
 {
     Write-Host "node information was not retrieved." -ForegroundColor Red
 }

 $jsonResponse = ConvertFrom-Json $response.Content

  return $jsonResponse
}
```

Замените параметр `Uri` на универсальный код ресурса (URI) опрашивающего сервера. Если вы хотите получать сведения об узле в формате XML, задайте для `ContentType` значение `application/xml`.

Чтобы извлечь сведения об узле из параметра `$json`, сделайте следующее:

```powershell
$json = QueryNodeInformation –Uri http://localhost:7070/PSDSCComplianceServer.svc/Status

$json.value | Format-Table TargetName, ConfigurationId, ServerChecksum, NodeCompliant, LastComplianceTime, StatusCode
```