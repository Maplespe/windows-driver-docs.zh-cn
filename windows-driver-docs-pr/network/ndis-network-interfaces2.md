---
title: NDIS 网络接口简介
description: NDIS 网络接口简介
ms.assetid: a1d062d4-3d4b-4244-b851-667d708810db
keywords:
- NDIS WDK, 网络接口
- NDIS 网络接口 WDK
- 网络接口 WDK
- NDISIF WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68388b8b41bb44897cdb193f6afefa9c243a9451
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565747"
---
# <a name="introduction-to-ndis-network-interfaces"></a>NDIS 网络接口简介

为了支持管理信息基础 (MIB), NDIS 管理本地计算机的网络接口信息集合。 NDIS 接口提供程序提供有关某些网络接口到 NDIS 的信息。 NDIS 提供一个代理接口提供程序, 该提供程序注册接口并处理微型端口适配器和筛选器模块的接口提供程序请求。 因此, 不需要任何 NDIS 驱动程序作为网络接口提供程序。

但是, 所有 NDIS 网络驱动程序类型都可以注册为接口提供程序。 此类驱动程序注册网络接口, 并提供回调函数以响应接口 OID 请求。 NDIS 接口提供程序通常提供有关不能直接访问 NDIS 并且不受 NDIS 代理接口提供程序支持的接口的信息。 例如, MUX 中间驱动程序可以在其虚拟微型端口和基础适配器之间具有内部接口。

本部分包括：

[NDIS 网络接口概述](overview-of-ndis-network-interfaces.md)

[注册为接口提供程序](registering-as-an-interface-provider.md)

[管理 NDIS 网络接口](managing-ndis-network-interfaces.md)

[在 NDIS 接口提供程序中处理 OID 查询和设置请求](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)

[将 NDIS 网络接口映射到 NDIS Oid](mapping-of-ndis-network-interfaces-to-ndis-oids.md)

 

 





