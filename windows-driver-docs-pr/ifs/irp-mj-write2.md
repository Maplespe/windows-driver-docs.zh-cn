---
title: 检查 IRP_MJ_WRITE 操作的 Oplock 状态
description: 检查 IRP_MJ_WRITE 操作的 Oplock 状态
ms.assetid: 04d09810-f157-4140-8bfb-c780a65cdf77
ms.date: 11/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 82fad40d1b288cc9be243a52fec8928955624f92
ms.sourcegitcommit: 79ff84ffc2faa5fdb3294e1fb5791f6a0ea7ef50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2019
ms.locfileid: "74543042"
---
# <a name="checking-the-oplock-state-of-an-irp_mj_write-operation"></a>检查 IRP_MJ_WRITE 操作的 Oplock 状态

在写入*流*并且写入不是分页 i/o 时，以下[oplock 中断](https://docs.microsoft.com/windows-hardware/drivers/ifs/breaking-oplocks)条件适用。

### <a name="conditions-for-a-level-2-request-type"></a>第2级请求类型的条件：

- 始终中断到无。

- 不需要确认;操作会立即继续。

### <a name="conditions-for-all-other-request-types"></a>所有其他请求类型的条件：

- 当在带有 oplock 密钥的某个 FILE_OBJECT 上发生写入操作时 IRP_MJ_WRITE 中断，该操作与拥有 oplock 的 FILE_OBJECT 的键不同。 如果 oplock 中断，则中断到无。

- 确认要求不同如下：

  - 读取请求：不需要确认;操作会立即继续。
  
  - 读取句柄请求：尽管需要确认中断，但操作会立即继续进行（例如，无需等待确认）。
  
  - 级别1、批处理、筛选器、读写和读写处理请求：必须先收到确认，然后才能继续操作。
