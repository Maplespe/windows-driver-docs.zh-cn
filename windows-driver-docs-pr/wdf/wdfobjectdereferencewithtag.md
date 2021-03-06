---
title: WdfObjectDereferenceWithTag 宏
description: WdfObjectDereferenceWithTag 宏递减指定框架对象的引用计数，并将驱动程序的当前文件名和行号分配给引用。 此宏还向引用分配标记值。
ms.assetid: c5cfe516-ad62-4656-a033-d1800d9554a8
keywords:
- WdfObjectDereferenceWithTag 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5e2af1195bf03fe3e875ff40b6a32c46b1efdf5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842411"
---
# <a name="wdfobjectdereferencewithtag-macro"></a>WdfObjectDereferenceWithTag 宏


\[适用于 KMDF 和 UMDF\]

**WdfObjectDereferenceWithTag**宏递减指定框架对象的引用计数，并将驱动程序的当前文件名和行号分配给引用。 此宏还向引用分配标记值。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID WdfObjectDereferenceWithTag(
  [in] WDFOBJECT Handle,
  [in] PVOID     Tag
);
```

<a name="parameters"></a>参数
----------

*处理*\] 中的 \[  
框架对象的句柄。

*标记*\[\]  
用于标识对象引用的驱动程序定义的值。 标记值必须匹配驱动程序以前提供给[**WdfObjectReferenceWithTag**](wdfobjectreferencewithtag.md)的标记值。

<a name="return-value"></a>返回值
------------

无。

如果驱动程序提供的对象句柄无效，则会发生 bug 检查。

<a name="remarks"></a>备注
-------

如果对象的引用计数变为零，则在**WdfObjectDereferenceWithTag**返回之前可能会删除该对象。

调用[**WdfObjectDereferenceActual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdereferenceactual)或**WdfObjectDereferenceWithTag**而不是[**WdfObjectDereference**](wdfobjectdereference.md)将向 Microsoft 调试器提供附加信息（标记字符串、行号和文件名）。 **WdfObjectDereferenceActual**允许驱动程序指定行号和文件名，而**WdfObjectDereferenceWithTag**使用驱动程序的当前行号和文件名。

可以通过使用 **！ wdftagtracker**调试器扩展来查看标记、行号和文件名值。 调试器扩展将标记值显示为指针和一系列字符。 有关调试器扩展的详细信息，请参阅[调试 KMDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)。

有关对象引用计数的详细信息，请参阅[框架对象生命周期](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)。

<a name="examples"></a>示例
--------

下面的代码示例将减小对象的引用计数，并为引用分配标记值。

```cpp
WdfObjectDereferenceWithTag(
                            object,
                            pTag
                            );
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">全局</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>最低 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wdfobject （包含 Wdf .h）</td>
</tr>
<tr class="odd">
<td><p>库</p></td>
<td>Wdf01000 （KMDF）;WUDFx02000 （UMDF）</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WdfObjectDereference**](wdfobjectdereference.md)

[**WdfObjectReferenceWithTag**](wdfobjectreferencewithtag.md)

 

 






