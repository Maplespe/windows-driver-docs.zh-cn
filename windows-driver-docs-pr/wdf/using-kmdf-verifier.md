---
title: 使用 KMDF 验证程序
description: 使用 KMDF 验证程序
ms.assetid: ab6a0149-9341-435b-b7e7-9c5d6520ebd8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac1e0d92cd2cc0ffd5f502e38eb6a962741a9347
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842129"
---
# <a name="using-kmdf-verifier"></a>使用 KMDF 验证程序


该框架提供了可用于测试正在运行的 KMDF 驱动程序的内置验证功能。 此功能称为 KMDF Verifier，广泛验证驱动程序的状态和驱动程序传递给框架对象方法的参数。 您可以单独使用框架的验证程序，也可以结合使用通用[驱动程序验证程序（verifier）](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)工具。

如果启用了 KMDF Verifier，框架将检查锁获取和层次结构，确保对框架的调用以正确的 IRQL 出现，验证正确的 i/o 取消和队列使用情况，并确保驱动程序和框架遵循记录的签订. 它还可以模拟内存不足的情况，以便驱动程序开发人员可以测试驱动程序是否正确响应，而无需崩溃、挂起或卸载。

如果启用了 KMDF 验证程序，则当默认超时期限为60秒时，框架会中断到调试器，直到前面介绍的某些事件完成。 此时，您可以调试问题，或在调试器中键入 "g" 来重新启动超时期限。 使用[控制验证程序行为](#controlling-the-verifiers-behavior)中所述的**DbgWaitForSignalTimeoutInSec**注册表值，可以更改默认超时期限。

建议在测试过程中运行驱动程序验证程序（Verifier），然后将自己的驱动程序和 wdf01000 添加到验证列表。

如果你的驱动程序是用 KMDF 版本1.9 或更高版本生成的，并且你运行的是 Verifier，则会自动启用 KMDF 验证程序。

你还可以使用[WDF 验证器控件应用程序（您尚未 wdfverifier）](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)来启用和禁用 KMDF verifier。

## <a name="enabling-and-disabling-the-frameworks-built-in-verification"></a>启用和禁用框架的内置验证


你可以使用以下过程手动启用 KMDF 验证程序：

1.  如果已加载了驱动程序，请使用设备管理器禁用该设备。 禁用该设备将导致卸载该驱动程序。
2.  使用 RegEdit 将**VerifierOn**设置为驱动程序的参数中的非零值 **\\** 项中的**HKEY\_本地\_机\\系统\\CurrentControlSet\\Services**密钥registry. 非零值表示启用了 KMDF Verifier。

    如果子项不存在，你可能需要手动将**VerifierOn**添加到该子项。

3.  使用设备管理器重新启用设备，从而加载驱动程序。
4.  当驱动程序调用[**WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)时，框架将检查注册表，如果**VerifierOn**为非零值，则会启用框架的验证程序。

若要禁用框架的验证程序，请执行相同的步骤，但将**VerifierOn**的值设置为零。

若要确定是否已启用框架的验证程序，请在驱动程序调用[**WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)后在某个位置设置断点，并使用[ **！ wdfdriverinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo)调试器扩展命令：

**！ wdfkd. wdfdriverinfo** *&lt;你的 drivername&gt;*  **** **0x1**

有关调试器扩展命令的详细信息，请参阅[基于框架的驱动程序的调试器扩展](debugger-extensions-for-kmdf-drivers.md)。

## <a name="controlling-the-verifiers-behavior"></a>控制验证程序的行为


建议使用[WDF 验证器控件应用程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)来控制以下选项。 但是，你可以直接修改注册表中的以下值。

相关值位于**HKEY\_本地\_机\\System\\CurrentControlSet\\Services**密钥的**参数\\Wdf**子项下。

<a href="" id="verifyon-----------------reg-dword-"></a>**VerifyOn** （**REG\_DWORD**）  
将此值设置为一个非零值，以启用[**WDFVERIFY**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfverify)宏。

<a href="" id="dbgbreakonerror-----------------------------reg-dword-"></a>**DbgBreakOnError** （**REG\_DWORD**）  
如果此值设置为非零值，则每次驱动程序调用[**WdfVerifierDbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)时，框架都将中断到调试器（如果可用）。

<a href="" id="dbgwaitforsignaltimeoutinsec---------------reg-dword-"></a>**DbgWaitForSignalTimeoutInSec** （**REG\_DWORD**）  
从 Windows 8 开始，当**VerifierOn**和**DbgBreakOnError**设置为非零值时，驱动程序可以通过设置**DbgWaitForSignalTimeoutInSec**来更改默认超时时间。

<a href="" id="verifierallocatefailcount------------------------------reg-dword-"></a>**VerifierAllocateFailCount** （**REG\_DWORD**）  
如果此值设置为值*n*，则在第*n*个分配后，框架将无法每次尝试为驱动程序的对象分配内存。

<a href="" id="trackhandles---------------reg-multi-sz-"></a>**TrackHandles** （**REG\_多\_SZ**）  
如果此值设置为框架对象句柄的一个或多个类型名称的列表，则框架将跟踪与指定的句柄类型匹配的所有对象句柄的引用。

<a href="" id="enhancedverifieroptions-----------------------------reg-dword-"></a>**EnhancedVerifierOptions** （**REG\_DWORD**）  
**仅 KMDF**

包含一个可用于启用框架的验证程序的可选功能的位图。

<a href="" id="verifydownlevel--------------reg-dword-"></a>**VerifyDownLevel** （**REG\_DWORD**）  
如果设置为非零值，并且该驱动程序是使用比当前版本旧的 framework 版本生成的，则该框架的验证程序将包含在生成驱动程序之后添加的测试。

一般规则是，如果设置上述注册表值，请在不再需要这些值时将其删除。

有关这些注册表值的完整说明，请参阅[用于调试基于框架的驱动程序的注册表值](registry-values-for-debugging-kmdf-drivers.md)。

 

 





