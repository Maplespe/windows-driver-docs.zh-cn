---
title: NDIS_STATUS_WWAN_UICC_APP_LIST
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_UICC_APP_LIST 通知来通知移动宽带（MB）服务完成了上一个 OID_WWAN_UICC_APP_LIST 查询请求。
ms.assetid: D18BA7C8-5CEC-4DF6-BB5A-C8F65E1911A5
ms.date: 04/08/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_UICC_APP_LIST 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 207b3775a8fed3def19dc698a774d6da9971a025
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844814"
---
# <a name="ndis_status_wwan_uicc_app_list"></a>NDIS_STATUS_WWAN_UICC_APP_LIST

微型端口驱动程序使用**NDIS_STATUS_WWAN_UICC_APP_LIST**通知来通知移动宽带（MB）服务完成了上一个[OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)查询请求。

未经请求的事件不适用。

此通知使用[**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | Windows 10 版本 1903 |
| 标头 | Ntddndis （包括 Ndis .h） |

## <a name="see-also"></a>另请参阅

[MB UICC 应用程序和文件系统访问](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)

[**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)
