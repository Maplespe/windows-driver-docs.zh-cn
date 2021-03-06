---
title: Bug Check 0x157 KERNEL_THREAD_PRIORITY_FLOOR_VIOLATION
description: ATTEMPTED_SWITCH_FROM_DPC bug 检查具有 0x00000157 值。 这表示在特定线程的优先级下限尝试了非法操作。
ms.assetid: 93D15A0A-1413-47DB-91E8-DB61A3604BB1
keywords:
- Bug Check 0x157 KERNEL_THREAD_PRIORITY_FLOOR_VIOLATION
- KERNEL_THREAD_PRIORITY_FLOOR_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_THREAD_PRIORITY_FLOOR_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e59062ab6ba025b9fe3d2b531017c89aad6af7c
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520038"
---
# <a name="bug-check-0x157-kernelthreadpriorityfloorviolation"></a>Bug 检查 0x157：内核\_线程\_优先级\_FLOOR\_冲突


已尝试\_交换机\_FROM\_DPC bug 检查的值为 0x00000157。 这表示在特定线程的优先级下限尝试了非法操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="kernelthreadpriorityfloorviolation-parameters"></a>内核\_线程\_优先级\_FLOOR\_冲突参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left">该线程的地址</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">目标优先级值</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left"><p>指示冲突原因的状态代码</p>
0x1:目标优先级的优先级计数器过度流入 0x2:目标优先级的优先级计数器下流入 0x3:是非法的目标优先级值</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">保留</td>
</tr>
</tbody>
</table>

 

 

 




