---
title: 简单的传递调度和完成示例
description: 简单的传递调度和完成示例
ms.assetid: dae3a450-37b1-470b-a0f3-4108075e06ac
keywords:
- IRP 完成例程 WDK 文件系统，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfcae8b6d968581e660060832441237c55be47f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841423"
---
# <a name="example-simple-pass-through-dispatch-and-completion"></a>示例：简单的传递调度和完成


## <span id="ddk_example_simple_pass_through_dispatch_and_completion_if"></span><span id="DDK_EXAMPLE_SIMPLE_PASS_THROUGH_DISPATCH_AND_COMPLETION_IF"></span>


若要为 IRP 设置完成例程并向下传递 IRP，调度例程必须执行以下操作：

-   调用[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) ，将参数从当前堆栈位置复制到下一个较低级别驱动程序的位置。

-   调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)为 IRP 指定完成例程。

-   调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，将 IRP 向下传递到下一个较低级别的驱动程序。

下面的代码示例演示了此方法：

### <a name="span-iddispatch_routinespanspan-iddispatch_routinespanspan-iddispatch_routinespandispatch-routine"></a><span id="Dispatch_Routine"></span><span id="dispatch_routine"></span><span id="DISPATCH_ROUTINE"></span>调度例程

```cpp
IoCopyCurrentIrpStackLocationToNext( Irp ); 
IoSetCompletionRoutine( Irp,                                 // Irp
                        MyLegacyFilterPassThroughCompletion, // CompletionRoutine
                        (PVOID)recordList,                   // Context
                        TRUE,                                // InvokeOnSuccess
                        TRUE,                                // InvokeOnError
                        TRUE);                               // InvokeOnCancel
return IoCallDriver ( NextLowerDriverDeviceObject, Irp ); 
```

在此示例中，对[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)的调用将为 IRP 设置完成例程。

调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)的前两个参数是一个指向 IRP 的指针和完成例程的名称。 第三个参数是指向要传递到完成例程的驱动程序定义的结构的指针。 此结构包含在 IRP 上执行完成处理时需要完成例程的上下文信息。 必须从非分页池分配上下文结构，因为完成例程可以在 IRQL 调度\_级别进行调用。

传递给[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)的最后三个参数是用于指定在 i/o 请求成功、失败或已取消时调用完成例程的标志。

### <a name="span-idcompletion_routinespanspan-idcompletion_routinespanspan-idcompletion_routinespancompletion-routine"></a><span id="Completion_Routine"></span><span id="completion_routine"></span><span id="COMPLETION_ROUTINE"></span>完成例程

如果派单例程设置完成例程，并在调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)之后立即返回（如上面的调度例程所示），则相应的完成例程必须检查 IRP 的 PendingReturned 标志，如果已设置，则调用**也**。 然后，它应返回成功\_状态，如以下示例中所示：

```cpp
if (Irp->PendingReturned) {
    IoMarkIrpPending( Irp );
}
return STATUS_SUCCESS;
```

### <a name="span-idadvantages_of_this_approachspanspan-idadvantages_of_this_approachspanspan-idadvantages_of_this_approachspanadvantages-of-this-approach"></a><span id="Advantages_of_This_Approach"></span><span id="advantages_of_this_approach"></span><span id="ADVANTAGES_OF_THIS_APPROACH"></span>此方法的优点

通过设置完成例程，驱动程序可以在由较低级别的驱动程序处理 IRP 后进一步对其进行处理。 完成例程可以决定如何根据请求的 i/o 操作的结果来处理 IRP。

### <a name="span-iddisadvantages_of_this_approachspanspan-iddisadvantages_of_this_approachspanspan-iddisadvantages_of_this_approachspandisadvantages-of-this-approach"></a><span id="Disadvantages_of_This_Approach"></span><span id="disadvantages_of_this_approach"></span><span id="DISADVANTAGES_OF_THIS_APPROACH"></span>此方法的缺点

由于它在任何线程上下文中以 IRQL &lt;= 调度\_级别运行，因此完成例程只能在 IRP 上执行有限的处理。

 

 




