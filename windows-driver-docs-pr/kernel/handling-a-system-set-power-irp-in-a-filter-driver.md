---
title: 处理筛选器驱动程序中的系统 Set-Power IRP
description: 处理筛选器驱动程序中的系统 Set-Power IRP
ms.assetid: a6e364fc-f173-47ce-b36b-84f802cefcc3
keywords:
- 设置电源 Irp WDK 电源管理
- 筛选器驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5a8eeb3550ffe44a933ca5812c5d034b8e33bf6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838672"
---
# <a name="handling-a-system-set-power-irp-in-a-filter-driver"></a>处理筛选器驱动程序中的系统 Set-Power IRP





所有筛选器驱动程序和不拥有其设备堆栈的电源策略的任何函数驱动程序都应该只需将系统设置-电源 IRP 传递到下一个较低的驱动程序，如下所示：

1.  调用[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)，传递当前 IRP，以确保驱动程序未收到 PnP [**IRP\_MN\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)在处理 power IRP 时删除\_设备请求。

    如果**IoAcquireRemoveLock**返回失败状态，驱动程序不应继续处理 IRP。 从 Windows Vista 开始，驱动程序应调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)来完成 IRP 并返回失败状态。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序应该首先调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)，然后调用**IOCOMPLETEREQUEST**来完成 IRP，然后返回失败状态。

2.  调用**PoStartNextPowerIrp**以启动下一个 power IRP。 （仅限 windows Server 2003、Windows XP 和 Windows 2000。）

3.  设置 IRP 堆栈位置（[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)或[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)）。 驱动程序可以在 IRP 中设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，但这样做很少需要。

4.  调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) （在 windows 7 和 windows Vista 中）或[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) （在 Windows SERVER 2003、windows XP 和 windows 2000 中）将 IRP 传递到下一个较低版本的驱动程序。

5.  调用[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)。 但是，如果驱动程序为 IRP 设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，则改为从*IoCompletion*例程进行此调用。

6.  返回状态从其[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程挂起\_。

 

 




