---
title: WDI_TLV_RADIO_STATE_PARAMETERS
description: WDI_TLV_RADIO_STATE_PARAMETERS 是包含单选状态参数的 OID_WDI_TASK_SET_RADIO_STATE TLV。
ms.assetid: D977DF8A-146C-4921-AE7C-5FBEC7FBA4C8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_RADIO_STATE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 84c5929034c5035357134743d666c5bab3ee860a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366512"
---
# <a name="wditlvradiostateparameters"></a>WDI\_TLV\_RADIO\_STATE\_PARAMETERS


WDI\_TLV\_单选\_状态\_参数是包含单选状态参数 TLV [OID\_WDI\_任务\_设置\_单选\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-set-radio-state)。

## <a name="tlv-type"></a>TLV 类型


0xA0

## <a name="length"></a>长度


超出 UINT8 的大小 （以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>所需的单选状态中。
<p>有效值为的 0 （单选处于关闭状态） 和 1 （启用单选）。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




