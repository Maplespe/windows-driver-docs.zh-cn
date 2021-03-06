---
title: PcRegisterAdapterPower 规则（音频）
description: PcRegisterAdapterPower 规则指定 PortCls 微型端口驱动程序不应调用 PcRegisterAdapterPowerManagement 两次，而不会对 PcUnregisterAdapterPowerManagement 调用 PcUnregisterAdapterPowerManagement。首先调用 PcRegisterAdapterPowerManagement。
ms.assetid: 8F6E6B1D-F19C-469A-BC5A-061996BEA532
ms.date: 05/21/2018
keywords:
- PcRegisterAdapterPower 规则（音频）
topic_type:
- apiref
api_name:
- PcRegisterAdapterPower
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 658cf524fd606f5c5d81109b39c7f8559b4db683
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839585"
---
# <a name="pcregisteradapterpower-rule-audio"></a>PcRegisterAdapterPower 规则（音频）


PcRegisterAdapterPower 规则指定 PortCls 微型端口驱动程序不应：

-   调用[**PcRegisterAdapterPowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement)两次，无需对[**PcUnregisterAdapterPowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement)调用干预。
-   请先调用[**PcUnregisterAdapterPowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement) ，然后再调用[**PcRegisterAdapterPowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement) 。

|              |       |
|--------------|-------|
| 驱动程序模型 | Audio |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查0xC4：检测到\_冲突的驱动程序\_验证程序\_** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) （0x00071006） |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定<strong>/domain 音频</strong>。</p>
<p>例如：</p>
<p><strong>verifier/domain 音频</strong>[<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





