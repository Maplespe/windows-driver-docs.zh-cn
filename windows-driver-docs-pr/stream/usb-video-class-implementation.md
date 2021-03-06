---
title: USB 视频类实现
description: USB 视频类实现
ms.assetid: b390d741-9ddc-4bac-bca2-73e32461c5ed
keywords:
- USB 视频类驱动程序 WDK AVStream，实现
- 视频类驱动程序 WDK USB，实现
- UVC 驱动程序 WDK AVStream，实现
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad0b41a3e1121083086a4abb8e6d2cce100b0b06
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842624"
---
# <a name="usb-video-class-implementation"></a>USB 视频类实现


Microsoft 提供的 USB 视频类驱动程序（usbvideo）是以 pin 为中心的 AVStream 微型驱动程序。 它为操作系统枚举的每个 USB 视频类的兼容设备实例创建筛选器工厂。 驱动程序还会为设备上的每个输入或输出终端创建一个 pin 工厂，并将[**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)结构的**数据流**成员设置为相关值。

USB 视频类驱动程序使用设备描述符报告的内部设备拓扑来构造由筛选器、节点和连接组成的内核流式处理（KS）拓扑图。

USB Video 类基于设备支持的控件数量和类型，通过 AVStream 筛选器和固定描述符中的 KS 自动化表动态报告筛选器、固定和节点属性集。

USB 视频类基于设备上每个视频或静止图像数据终结点支持的数据格式，报告了所支持的 KS 数据范围的相应列表，以及相应的 AVStream pin 描述符中的数据交集处理程序。 USB 视频类驱动程序通过[内核流式处理代理](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)模块导出信息。

USB 视频类驱动程序还支持音频/视频流同步;usbvideo 可以用作 KS 主机时钟，并向视频示例添加时间戳。 USB 视频类规范包含有关硬件应如何向类驱动程序提供计时信息的详细信息。

若要与 USB Video 类通信，用户模式客户端将调用 DirectShow 或媒体基础接口。 这些接口是由内核流式处理代理作为插件定义的 COM 接口包装器。有关[媒体基础](https://go.microsoft.com/fwlink/p/?linkid=144771)的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




