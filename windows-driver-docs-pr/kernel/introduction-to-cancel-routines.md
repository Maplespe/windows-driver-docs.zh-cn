---
title: Cancel 例程简介
description: Cancel 例程简介
ms.assetid: 99f7f045-2b2f-4fb3-ac1c-99ab76fa46ad
keywords:
- 正在取消 Irp，关于取消 Irp
- 取消例程，关于取消例程
- 关联的 IRP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac1db60e183a61d4a4c7cf9d50dadf9ef5986717
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838634"
---
# <a name="introduction-to-cancel-routines"></a>Cancel 例程简介





任何可能处于无限间隔状态的 Irp 都处于挂起状态的驱动程序必须具有一个或多个[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程。 例如，键盘驱动程序可能会无限期地等待用户按下某个键。 相反，如果驱动程序将不会将更多的 Irp 排队超过5分钟，则它可能不需要*取消*例程。

假设用户模式线程发出 i/o 请求，该请求由最高级别的设备驱动程序的调度例程排队，并在 IRP 排队时终止请求的线程。 应取消代表终止的线程排队的 Irp。 因此，驱动程序必须在它所排队的每个 IRP 中设置驱动程序提供的*取消*例程。

当主 IRP 取消时，创建关联的 Irp 的驱动程序必须将其取消。 由于关联的 Irp 不与请求线程关联，因此在取消 master IRP 时，master IRP 的*Cancel*例程负责取消任何关联的 irp。

任何驱动程序的*取消*例程数取决于驱动程序的设计。 通常情况下，驱动程序应在其 i/o 处理中的每个阶段都有一个*取消*例程，此时 IRP 可能处于无限期的挂起状态。 此类挂起的 Irp 被视为*处于*可取消状态。

请考虑以下设计准则：

-   如果分层驱动程序链中的最高级别的驱动程序对 Irp 进行排队或以可取消状态保存 Irp，则必须至少具有一个*Cancel*例程。 必要时，它可以有多个*取消*例程。

-   可在相对较长的时间间隔内保持 Irp 处于可取消状态的底层驱动程序还应具有一个或多个*取消*例程。

-   如果驱动程序管理自己的 Irp 的内部队列，则该驱动程序的每个队列应有单独的*取消*例程。

对于交互式设备（例如键盘、鼠标、声音、并行类和串行驱动程序），某些最高级别的驱动程序必须包含*取消*例程。 某些较低级别的驱动程序（如并行端口驱动程序）会将 Irp 排队等候更长的时间间隔，还应具有*取消*例程。

大容量存储设备驱动程序以及其上分层的中间驱动程序不大可能具有*取消*例程。 文件系统驱动程序负责处理对文件 i/o 请求的取消操作，而较低级别的大容量存储驱动程序的 Irp 输入通常处理得太快，无法取消。

 

 




