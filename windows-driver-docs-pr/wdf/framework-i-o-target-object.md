---
title: 框架 I/O 目标对象
description: 框架 I/O 目标对象
ms.assetid: 355a1818-88c9-4989-9141-8445f511f501
keywords:
- UMDF 对象 WDK，i/o 目标对象
- framework 对象 WDK UMDF，i/o 目标对象
- I/o 目标对象 WDK UMDF
- IWDFIoTarget
- 目标 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50da71595f7edc35dedd826575c9e78e46ba4e6a
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210359"
---
# <a name="framework-io-target-object"></a>框架 I/O 目标对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架 i/o 目标对象通过[IWDFIoTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget)接口向驱动程序公开。 它检索有关 i/o 目标的信息，这通常表示堆栈中较低的驱动程序，但也可以表示堆栈中的另一个 UMDF 驱动程序或内核模式部分。 I/o target 对象为 UMDF 驱动程序提供了一种将请求发送到其他设备的方法。

UMDF 驱动程序还可以使用[IWDFIoTargetStateManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotargetstatemanagement)接口来管理和监视 i/o 目标对象的状态。

 

 





