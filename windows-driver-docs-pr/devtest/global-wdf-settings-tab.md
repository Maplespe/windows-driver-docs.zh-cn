---
title: 全局 WDF 设置选项卡
description: 本主题提供了 WDF 验证程序的全局 WDF 设置页的详细的信息。 此页提供了全局 （系统范围内） WDF 验证选项，并显示与托管驱动程序 UMDF 主机进程。
ms.assetid: 9b976a59-329f-41a7-9eff-8f18d75cdb42
keywords:
- WDF 验证程序 WDK，管理 UMDF 设置
- WDK WDF 的 UMDF 验证程序设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbda0fa0b8e75c332ed3c5f0d92c4349d8405e02
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358303"
---
# <a name="global-wdf-settings-tab"></a>全局 WDF 设置选项卡


本主题提供有关 WDF 验证程序的详细的信息**全局 WDF 设置**页。 此页提供了全局 （系统范围内） WDF 验证选项，并显示与托管驱动程序 UMDF 主机进程。

在顶部，您将看到**加载程序诊断的输出控制**框。 在这里，可以指定是否想要查看从 KMDF 和 UMDF 2.0 加载程序的诊断消息。 这些是全局的诊断 （DbgPrint 启用） 标志设置为各自的加载程序的选项。

![方全局 wdf 设置选项卡的屏幕截图](images/wdfverifier-tab3.png)

此外可以选择你想要看到加载程序内核调试程序中的诊断消息。

例如，如果使用用户模式下调试程序调试 UMDF 驱动程序，请为 UMDF 启用加载程序输出。 如果你正在调试 UMDF 驱动程序使用内核调试程序，还选择**使加载程序的诊断消息在内核调试器中看到**。

**主机进程**，将显示所有主机进程和其进程 Id，以及是否应用程序验证器处于活动状态的每个进程。 您可以展开或折叠每个进程中承载的驱动程序列表。 如果已在指定用户模式调试器[我的首选项](my-preferences-tab.md)页上，您可以还突出显示的驱动程序或进程，然后单击**用户模式下调试程序附加到此进程**按钮。

最后，**全局用户模式下验证器设置**框包含会影响系统上的所有 UMDF 驱动程序的调试选项。 有关这些设置的详细信息，请参阅[使用 UMDF Verifier](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-umdf-verifier)。

当对 UMDF 验证器设置进行更改时，这些更改会影响随后加载的设备。 如果你的设备已在运行，必须禁用并重新启用它。 WDF 验证程序禁用和重新启用该设备，为，如果更改 UMDF 跟踪级别或 select**将日志输出将发送到内核调试程序**选项。 如果选择此选项不工作**不采取任何操作...** 在**必须重新启动计算机...** 上的下拉列表[我的首选项](my-preferences-tab.md)页。

**若要设置的用户模式下调试程序自动启动**

1.  请确保上指定了用户模式调试器[我的首选项](my-preferences-tab.md)页。
2.  指定在驱动程序加载延迟或新的主机进程的开始时间。 在延迟应至少为两秒。
3.  选择**自动启动请求时的用户模式下调试器**，然后单击**应用**。
4.  将保留 WDF 验证程序运行。 新的主机进程启动时，WDF 验证程序会将你要使用的调试器附加到进程。
5.  如果您的驱动程序已在运行，更改跟踪级别，或选择**发送日志输出到内核调试器**然后单击**应用**。 这样做会停止并重新启动所有 UMDF 进程，除非你是关闭自动重新启动功能 (您可以将其还原上[我的首选项](my-preferences-tab.md)页)。

 

 





