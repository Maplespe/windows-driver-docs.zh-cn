---
title: Bug 检查 0x7F UNEXPECTED_KERNEL_MODE_TRAP
description: UNEXPECTED_KERNEL_MODE_TRAP bug 检查具有 0x0000007F 值。
ms.assetid: f4fcc2a1-891b-44e9-94bf-e712019f538f
keywords:
- Bug 检查 0x7F UNEXPECTED_KERNEL_MODE_TRAP
- UNEXPECTED_KERNEL_MODE_TRAP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- UNEXPECTED_KERNEL_MODE_TRAP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 63ed5fb19655c803119f4c35b429bfb8b9defb01
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519170"
---
# <a name="bug-check-0x7f-unexpectedkernelmodetrap"></a>Bug 检查 0x7F：意外\_内核\_模式\_陷阱


意外\_内核\_模式\_陷阱 bug 检查的值为 0x0000007F。 此 bug 检查指示生成的 Intel CPU 陷阱，内核未能捕获此陷阱。

可能是此陷阱*绑定的陷阱*（陷阱内核不允许捕获） 或*双容错*（处理总是会导致系统出现故障的早期错误时出现的错误）。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="unexpectedkernelmodetrap-parameters"></a>意外\_内核\_模式\_陷阱参数


在蓝色屏幕显示的第一个参数指定陷阱数。

最常见的陷阱代码如下所示：

-   0x00000000 或被除零错误，指示执行 DIV 指令和除数为零。 内存损坏、 其他硬件问题或软件故障可能导致此错误。

-   0x00000004 或溢出，当处理器设置溢出 (OF) 标志时执行中断处理程序调用时发生。

-   0x00000005 或边界检查错误，指示，处理器执行绑定的指令时找到操作数超过了指定的限制。 绑定的指令可确保特定范围内是有符号的数组索引。

-   0x00000006 或无效的操作码，指示尝试执行无效的指令处理器。 通常，当指令指针已损坏，指向错误的位置时，将发生此错误。 此错误的最常见原因是硬件内存损坏。

-   0x00000008 或双精度错误，指示以前的异常的处理程序的调用过程中发生异常。 通常情况下，两种例外情况是按顺序处理。 但是，有几个例外情况，不能按顺序处理，并在此情况下处理器发出信号的双精度错误。 有两个常见原因的双精度错误：
    -   内核堆栈溢出。 当命中一个保护页，并尝试推送陷阱帧内核时，会发生此溢出。 由于不没有保留任何堆栈，结果的堆栈溢出，从而导致双精度错误。 如果您认为发生此概述，请使用[ **！ 线程**](-thread.md)来确定堆栈限制，然后使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)使用大型参数 (例如， **kb 100**) 以显示完整的堆栈。
    -   硬件问题。

不太常见陷阱代码如下所示：

-   0x00000001-系统调试器调用

-   0x00000003-调试器断点

-   0x00000007-存在没有协处理器的硬件协处理器指令

-   0x0000000A-一个损坏任务状态段

-   0x0000000B-对不存在的一个内存段的访问权限

-   0x0000000C-对堆栈的限制以外的内存的访问权限

-   0x0000000D-未涵盖的某些其他异常; 异常适用于应用程序的访问冲突保护错误

有关其他陷阱号，请参阅 Intel 体系结构手动。

<a name="cause"></a>原因
-----

Bug 检查 0x7F 通常会发生安装错误或不匹配的硬件 （尤其是内存中） 之后或如果安装的硬件无法正常工作。

内核堆栈溢出时，可能出现双故障。 如果多个驱动程序附加到相同的堆栈，则会出现此溢出。 例如，如果两个文件系统筛选器驱动程序附加到同一个堆栈，然后文件系统 recurses 回时，堆栈溢出。

<a name="resolution"></a>分辨率
----------

**调试：** 始终以开头[ **！ 分析**](-analyze.md)扩展。

如果此扩展不充分，请使用[ **kv （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)调试器命令。

-   如果**kv**演示**taskGate**，使用[ **.tss （显示任务状态段）** ](-tss--display-task-state-segment-.md)冒号之前的部分命令。

-   如果**kv**显示了陷阱框架，使用[ **.trap （显示陷阱帧）** ](-trap--display-trap-frame-.md)命令格式化帧。

-   否则，请使用[ **.trap （显示陷阱帧）** ](-trap--display-trap-frame-.md)命令相应帧上。 (在基于 x86 的平台上，此框架是与该过程关联**NT ！KiTrap**。)

使用以下命令之一之后, 使用**kv**再次以显示新的堆栈。

**故障排除：** 如果你最近添加到计算机的硬件，删除它以查看错误重复出现。 如果现有硬件出现故障，删除或更换有故障的组件。 运行硬件诊断系统制造商提供的可确定哪些硬件组件失败。

内存扫描程序来说尤其重要。 内存故障或不匹配可能会导致此 bug 检查。 有关这些过程的详细信息，请参阅您的计算机的用户手册。 检查计算机中的所有适配器卡正确就都位。 使用墨迹橡皮擦或电力联系处理方法，可在电子用品商店，以确保适配器卡联系人是干净。

如果此错误出现在新安装的系统上，检查可用的更新 BIOS，SCSI 控制器，或网络卡。 BBS 硬件制造商的网站上通常可用的更新这些种类。

确认所有硬盘驱动器、 硬盘控制器和 SCSI 适配器都是与安装的 Windows 版本兼容。 例如，可以获取有关与 Windows 7 的兼容性信息[Windows 7 兼容性中心](https://go.microsoft.com/fwlink/p/?LinkID=246806)。

如果错误发生的一个新的或更新设备驱动程序安装完成后，应删除或替换驱动程序。 如果在此情况下，在发生该错误启动序列和系统分区使用 NTFS 进行格式化，您可能能够使用安全模式下重命名或删除错误的驱动程序。 如果驱动程序用作在安全模式下在系统启动过程的一部分，您必须使用恢复控制台访问该文件以启动计算机。

此外重新启动计算机，并在基于字符的菜单显示操作系统选项按 F8。 在**高级选项**菜单中，选择**最后一个已知的正确配置**选项。 添加一次只能有一个驱动程序或服务时，此选项是最有效。

超频 （设置要在上面的已评分的规范的速度运行的 CPU） 可能会导致此错误。 如果您具有对超频计算机遇到错误，返回到默认时钟速度设置 CPU。

检查事件查看器中的系统日志可能有助于识别设备或导致错误的驱动程序的其他错误消息。 此外可以禁用内存中缓存的 BIOS 来尝试解决该问题。

如果在升级到新版本的 Windows 操作系统时遇到此错误，可能被导致错误的设备驱动程序、 系统服务、 病毒扫描程序或与新的版本不兼容的备份工具。 如果可能，请删除所有第三方设备驱动程序和系统服务，并在升级之前禁用任何病毒扫描程序。 请联系软件制造商以获取这些工具的更新。 此外请确保已安装最新的 Windows Service Pack。

最后，如果所有上述步骤未解决此错误，则可转到一个修复工具，以便诊断测试系统主板。 破裂、 污损的跟踪或在主板上的有故障组件也会导致此错误。

 

 




