---
title: ACPI_METHOD_SET_ARGUMENT_STRING 宏
description: ACPI_METHOD_SET_ARGUMENT_STRING 宏为字符串值设置 ACPI_METHOD_ARGUMENT 结构的成员。
ms.assetid: e0c037a9-65b6-4d6a-9ed6-d9296c14df07
keywords:
- ACPI_METHOD_SET_ARGUMENT_STRING 宏 ACPI 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e5d6746ee931adde6a75860a2fe1eea0e7f3194
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824056"
---
# <a name="acpi_method_set_argument_string-macro"></a>ACPI\_方法\_集\_参数\_字符串宏


ACPI\_方法\_SET\_参数\_字符串宏为字符串值设置[**ACPI\_方法\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)结构的成员。

<a name="syntax"></a>语法
------

```cpp
void ACPI_METHOD_SET_ARGUMENT_STRING(
    Argument,
    StrData
);
```

<a name="parameters"></a>参数
----------

*参数*   
指向 ACPI\_方法\_参数结构的指针。

*StrData*   
指向以 NULL 结尾的 ASCII 字符串的指针。

<a name="return-value"></a>返回值
------------

此宏不返回值。

<a name="remarks"></a>备注
-------

驱动程序可以使用此宏将 ACPI\_方法\_参数结构的成员设置为提供以 NULL 结尾的 ASCII 字符串。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr>
<td><p>目标平台</p></td>
<td>桌面设备</td>
</tr>
<tr>
<td><p>标头</p></td>
<td>Acpiioct （包括 Acpiioct）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**ACPI\_方法\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 
