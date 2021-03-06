---
title: 千兆位以太网网络适配器的电源管理注意事项
description: 千兆位以太网网络适配器的电源管理注意事项
ms.assetid: f195d295-0a2a-4c44-a3b4-217dfad76826
keywords:
- 电源管理 WDK 网络的千兆位以太网 Nic
- 网络接口卡 WDK 网络，转换的电源状态
- Nic WDK 网络，转换的电源状态
- Nic WDK 网络的千兆位以太网 Nic
- 网络接口卡 WDK 网络、 千兆位以太网 Nic
- 千兆位以太网 Nic WDK 网络
- 电源管理 WDK NDIS 微型端口转换的电源状态
- 设备电源状态 WDK 网络
- 电源状态 WDK 网络
- 转换电源状态 WDK 网络
- 唤醒功能 WDK 网络，转换的电源状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fffc18ddc49631b2fd491bf8adbbfa138e68803
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383171"
---
# <a name="power-management-considerations-for-gigabit-ethernet-network-adapters"></a>千兆位以太网网络适配器的电源管理注意事项


当在 1000 兆位 / 秒 (Mbps) 运行时的千兆位以太网网络适配器时，它可绘制电力很的多。 此类的网络适配器将转换为低功耗状态之前，其链接速度通常会降低，使网络适配器绘制较少的电量。 减少了的链接速度可以转换为低功耗状态的网络适配器。 而不断变化的链接转换的过程为低功耗状态，速度的网络适配器通常失去网络连接在短时间。

相反，在从低功耗状态转换为完全在状态中的千兆位以太网网络适配器，网络适配器链接速度被增加到其完全可操作的速率。 此转换期间的网络适配器可能还会丢失在短时间的连接。

虽然微型端口驱动程序的基础网络适配器正在转换到或从低功耗状态，微型端口必须指示链接速度中的更改或连接状态中的更改。 该值指示链接速度中的更改的详细信息，请参阅[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)。 该值指示连接状态中的更改的详细信息，请参阅[，该值指示连接状态](indicating-connection-status.md)。

 

 





