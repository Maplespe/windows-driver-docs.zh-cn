---
title: 适用于家庭影院系统的多声道格式
description: 适用于家庭影院系统的多声道格式
ms.assetid: b8bd1dc7-c9a8-4f4f-8014-d31f1ae5361a
keywords:
- 数据格式化 WDK 音频
- 格式化 WDK 音频、数据
- 音频数据格式 WDK
- 格式化 WDK 音频，多通道
- 多通道格式 WDK 音频
- 家庭影院系统 WDK 音频
- 扬声器 WDK 音频，threater 系统
- 音频驱动程序 WDK，家庭影院系统
- WDM 音频驱动程序 WDK，家庭影院系统
- 7.1 家庭影院扬声器 WDK 音频
- 7.1 宽配置扬声器 WDK 音频
- 宽配置扬声器 WDK 音频
- 5.1 环绕声扬声器 WDK 音频
- 环绕声扬声器
- 索尼动态数字声音
- SDD 配置 WDK 音频
- 流格式化 WDK 音频、多通道
- 定位 WDK 音频
- WDM 音频数据格式 WDK
- 数据格式化 WDK 音频，多通道
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7581ddf1d7538fff5bcc1e77d657e2af3a371db2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830368"
---
# <a name="multichannel-formats-for-home-theater-systems"></a>适用于家庭影院系统的多声道格式


家庭影院系统相对便宜的解决方案是，将一组环绕声扬声器连接到运行 Windows 操作系统的计算机上的音频适配器。 或者，用户可以在适配器输出与扬声器之间连接外部音频/视频（A/V）接收器。 为了应对家庭影院系统的受欢迎度，已为这些系统创作的5.1 和7.1 声道音频内容变得越来越多。

若要在家庭影院系统上准确渲染多通道音频内容，需要一个可将扬声器位置分配给多通道流中的音频通道的音频格式描述符。 如前文所述， [**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)结构可以指定此类扬声器分配。

为了帮助提供适用于家庭影院系统的音频驱动程序支持，Microsoft 为 Microsoft Windows XP 和更高版本定义了新的7.1 通道扬声器配置。 Windows Vista、带有 Service Pack 2 （SP2）的 windows XP 和带有 Service Pack 1 （SP1）的 Windows Server 2003 支持此配置。 在未安装 service pack 的 Windows Server 2003、带有 Service Pack 1 的 Windows XP 或未安装 service pack 的 Windows XP 中，不支持此方法。

下图显示了新的7.1 通道扬声器配置，该图是从 Windows XP SP2 中的 Windows 多媒体控制面板（Mmsys）获取的。

![新的7.1 声道扬声器配置图 ](images/spkrcfg1new.gif)

Windows 多媒体控制面板会将名称 "7.1 home 影院扬声器" 分配给上图中显示的新的7.1 声道范围的扬声器配置。

下图显示了 Windows 2000 和更高版本以及 Windows Me/98 中受支持的旧7.1 通道配置。

![较旧的7.1 信道范围配置图](images/spkrcfg1old.gif)

在带有 SP2 的 Windows XP 中，多媒体控制面板会将名称 "7.1 宽配置发言人" 分配给上图中显示的旧配置。

在带有 SP2 的 Windows XP 中，可以通过执行以下步骤来查找前面两个图形中所示的两个配置：

1.  在 "控制面板" （类别视图）中，单击 "**声音、语音和音频设备**"。

2.  在 "**声音、语音和音频设备**" 窗格的 "**选择任务**" 下，单击 "**调整系统音量**"。

3.  在 "**声音和音频设备属性**" 属性页的 "**音量**" 选项卡上的 "**扬声器设置**" 下，单击 "**高级**"。

4.  在 "**高级音频属性**" 属性表的 "**扬声器设置**" 下，打开下拉列表，并选择两个7.1 扬声器配置之一。

7\.1 宽配置音箱图中所示的配置是索尼动态数字音频（SDD）配置，在1993中引入，用于运动电影院。 不过，如果有很少的家庭影院系统，则使用此配置。 8个扬声器的家庭影院系统可能使用 7.1 Home 音箱扬声器中所示的新7.1 配置。 此外，还为 SDD 配置创作了最少的家庭影院内容，用户可能希望为新的7.1 配置格式化大部分可用的7.1 频道内容。

尽管新的 "7.1 home 电影院发言人" 配置基本上取代了旧的 "7.1 范围配置发言人" 配置，但 Windows 仍将继续支持旧配置，以提供向后兼容性。

在 Windows 2000 和更高版本以及 Windows Me/98 中，5.1 通道扬声器配置将通道5和6分别分配给左右扬声器。 在 Windows Vista、Windows Server 2003 SP1 和 Windows XP SP2 中，5.1 通道配置保持不变。 与7.1 通道配置相比，这些 Windows 版本不定义新的5.1 格式描述符来区分5.1 端扬声器配置和5.1 后扬声器配置。 由于这两种配置如此相似，因此，定义两个5.1 配置可能会导致用户之间出现混淆，这与要使用哪些配置有关，以及是否播放为其他配置上的一个配置创作的内容有关。 在6个扬声器的家庭影院系统中定位扬声器时，用户倾向于区分前后扬声器位置。 相反，演讲者定位更有可能由房间的形状和房间中的家具位置确定。

下图显示了5.1 声道环绕声扬声器配置，该图取自 Windows XP SP2 中的 Windows 多媒体控制面板。

![5\.1 声道环绕声扬声器配置 ](images/spkrcfg2.gif)

Windows 多媒体控制面板会将名称 "5.1 环绕声扬声器" 分配给上图中显示的5.1 声道配置。

尽管5.1 通道端扬声器和后扬声器配置之间的差异可能对用户是透明的，但它们对于音频硬件供应商并不透明。 如前所述，5.1-渠道内容通常是为侧扬声器而不是针对后扬声器创作的。 因此，在通过 "7.1 home 电影院发言人" 配置来播放5.1 频道内容时，供应商应确保5.1 通道流中的两个侧扬声器通道贯穿着扬声器，而不是后退扬声器。 同样，在使用侧扬声器通过5.1 发言人配置为 "7.1 家庭影院发言人" 配置播放的内容时，7.1 端扬声器的频道最自然映射到5.1 配置中的侧面扬声器。 对于具有流式处理功能的音频设备，另一种替代方法是让设备在5.1 配置中通过侧面发言人混合通道6和7之前，尝试保留通道4和5中的内容。

本部分包括：

[通道掩码](channel-mask.md)

[将流格式映射到发言人配置](mapping-stream-formats-to-speaker-configurations.md)

[标头文件更改](header-file-changes.md)

 

 




