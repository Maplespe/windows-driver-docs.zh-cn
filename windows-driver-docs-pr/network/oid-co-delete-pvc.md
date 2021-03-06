---
title: OID_CO_DELETE_PVC
description: 本主题介绍 OID_CO_DELETE_PVC 对象标识符（OID）。
ms.assetid: 02da08d0-9d08-4a91-b851-50e3c3b065d6
keywords:
- OID_CO_DELETE_PVC
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01098387d069bf42f92fb8e5c028f18e8c9689ef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843266"
---
# <a name="oid_co_delete_pvc"></a>OID_CO_DELETE_PVC

OID_CO_DELETE_PVC OID 由客户端发送到呼叫管理器，以便从已配置的 Pvc 的呼叫管理器列表中删除永久虚拟连接（PVC）。 PVC 的格式为 CO_PVC 结构，定义如下：

```c++
typedef struct _CO_PVC {
    NDIS_HANDLE             NdisAfHandle;
    CO_SPECIFIC_PARAMETERS  PvcParameters;
} CO_PVC, *PCO_PVC;
``` 

此结构的成员包含以下信息：

**NdisAfHandle**  
指定由[NdisClOpenAddressFamilyEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)返回的 NDIS 提供的句柄。

**PvcParameters**  
格式[CO_SPECIFIC_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)结构。 此结构包含用于描述 PVC 的特定于协议的参数。

管理员手动删除 PVC。 监视此类活动的客户端会向调用管理器发送此 OID，通知已删除的 PVC 的调用管理器。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis （包括 Ndis .h） |

