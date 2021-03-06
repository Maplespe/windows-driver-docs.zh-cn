---
title: Bug 检查 0x149 REFS_FILE_SYSTEM
description: REFS_FILE_SYSTEM bug 检查具有 0x00000149 值。 这表示发生文件系统错误。
ms.assetid: 899E89E7-46CD-4143-B1DC-7959F01643CF
keywords:
- Bug 检查 0x149 REFS_FILE_SYSTEM
- REFS_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REFS_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f45bc331b55b1e3213809692eb600607c73fc796
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520098"
---
# <a name="bug-check-0x149-refsfilesystem"></a>Bug 检查 0x149：REFS\_文件\_系统


REFS\_文件\_检查系统错误的值为 0x00000149。 这表示发生文件系统错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="refsfilesystem-parameters"></a>REFS\_文件\_系统参数


| 参数 | 描述                          |
|-----------|--------------------------------------|
| 1         | \_\_LINE\_\_                         |
| 2         | ExceptionRecord                      |
| 3         | ContextRecord                        |
| 4         | ExceptionRecord-&gt;ExceptionAddress |

 

| 参数 | 描述 |
|-----------|-------------|
| 1         | Message     |
| 2         | 保留    |
| 3         | 保留    |
| 4         | 保留    |

 

<a name="resolution"></a>分辨率
----------

如果在堆栈上看到 RefsExceptionFilter 然后第二个和第三个参数是异常记录和上下文记录。 不要[ **.exr** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-exr--display-exception-record-)第二个参数，以查看异常信息，然后执行[ **.cxr** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-cxr--display-context-record-)上的第三参数和[**kb** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)以获取更详细的堆栈跟踪。

 

 




