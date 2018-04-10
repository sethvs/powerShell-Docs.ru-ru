---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс nxSshAuthorizedKeys в DSC для Linux
ms.openlocfilehash: a36d158735839727e98893ce9fce174a0f37f764
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-for-linux-nxsshauthorizedkeys-resource"></a>Ресурс nxSshAuthorizedKeys в DSC для Linux

Ресурс **NxAuthorizedKeys** в DSC PowerShell обеспечивает механизм управления авторизованными SSH-ключами для указанного пользователя.

## <a name="syntax"></a>Синтаксис

```
nxAuthorizedKeys <string> #ResourceName
{
    KeyComment = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Username = <string> ]
    [ Key = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Свойства

|  Свойство |  Описание |
|---|---|
| KeyComment| Уникальный комментарий к ключу. Используется для уникальной идентификации ключей.|
| Ensure| Указывает, определен ли ключ. Если это свойство имеет значение Absent, обеспечивается отсутствие ключа в файле авторизованных ключей пользователя. Если это свойство имеет значение Present, обеспечивается наличие определения ключа в файле авторизованных ключей пользователя.|
| Имя пользователя| Указывает, для какого пользователя осуществляется управление авторизованными SSH-ключами. Если свойство не определено, пользователь по умолчанию — root.|
| Клавиши| Указывает содержимое ключа Требуется, если свойство **Ensure** имеет значение Present.|
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Пример

В следующем примере определяется общедоступный авторизованный SSH-ключ для пользователя monuser.

```
Import-DSCResource -Module nx

Node $node {

nxSshAuthorizedKeys myKey{
   KeyComment = "myKey"
   Ensure = "Present"
   Key = 'ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEA0b+0xSd07QXRifm3FXj7Pn/DblA6QI5VAkDm6OivFzj3U6qGD1VJ6AAxWPCyMl/qhtpRtxZJDu/TxD8AyZNgc8aN2CljN1hOMbBRvH2q5QPf/nCnnJRaGsrxIqZjyZdYo9ZEEzjZUuMDM5HI1LA9B99k/K6PK2Bc1NLivpu7nbtVG2tLOQs+GefsnHuetsRMwo/+c3LtwYm9M0XfkGjYVCLO4CoFuSQpvX6AB3TedUy6NZ0iuxC0kRGg1rIQTwSRcw+McLhslF0drs33fw6tYdzlLBnnzimShMuiDWiT37WqCRovRGYrGCaEFGTG2e0CN8Co8nryXkyWc6NSDNpMzw== rsa-key-20150401'
   UserName = "monuser"
}
}
```