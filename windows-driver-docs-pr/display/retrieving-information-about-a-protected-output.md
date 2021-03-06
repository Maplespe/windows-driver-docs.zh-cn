---
title: 检索有关受保护输出的信息
description: 检索有关受保护输出的信息
ms.assetid: 20e268b8-fea0-48dd-a3cd-3cbb4233ef99
keywords:
- OPM WDK 显示，检索受保护的输出信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14c8cea6a9360fbe4ba75ef86a97bc07dbf25630
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829574"
---
# <a name="retrieving-information-about-a-protected-output"></a>检索有关受保护输出的信息


显示微型端口驱动程序可以接收请求，以检索与图形适配器的物理输出连接器关联的受保护输出的相关信息。 显示微型端口驱动程序的[**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)函数将被传递到 DXGKMDT\_OPM 的指针\_在包含信息请求的*PARAMETERS*参数中[**获取\_信息\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_get_info_parameters)结构。 *DxgkDdiOPMGetInformation*会将所需的信息写入\_*RequestedInformation*参数所指向的[**信息结构\_\_OPM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_requested_information) 。 DXGKMDT\_OPM\_的**guidInformation**和**abParameters**成员获取\_信息\_参数指定信息请求。 根据信息请求，显示微型端口驱动程序应填充[**DXGKMDT\_OPM 的成员\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)、 [**DXGKMDT\_OPM\_输出\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_output_id)或[**DXGKMDT\_OPM\_实际\_输出\_格式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)结构和所需的信息，并将 ABREQUESTEDINFORMATION\_DXGKMDT\_请求\_信息的**OPM**成员指向该结构. 驱动程序指定**cbRequestedInformationSize** （例如，SIZEOF （DXGKMDT\_OPM\_标准\_信息））并**abRequestedInformation**成员 DXGKMDT\_OPM\_请求的\_信息时，驱动程序必须为 OMAC 中的数据计算一个密钥密码块链（CBC）模式消息身份验证代码（DXGKMDT）（OPM）。DXGKMDT\_OPM\_请求\_的信息。\_\_\_ 有关计算 OMAC 的详细信息，请参阅[OMAC 算法](https://go.microsoft.com/fwlink/p/?linkid=70417)。

**注意**   在[**DxgkDdiOPMGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)返回之前，显示微型端口驱动程序必须验证在 DXGKMDT\_OPM 的**OMAC**成员中指定的 OMAC [ **\_获取\_信息\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_get_info_parameters)是否正确。 驱动程序还必须验证在 DXGKMDT\_OPM 的**ulSequenceNumber**成员中指定的序列号是否\_获取\_信息\_参数与驱动程序当前已存储的序列号匹配。 然后，该驱动程序必须递增存储的序列号。

 

**请注意**   驱动程序必须在 DXGKMDT\_OPM 的**rnRandomNumber**成员中返回128位加密的安全随机数，\_标准\_信息、 [**DXGKMDT\_OPM\_输出\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_output_id)或 DXGKMDT\_OPM\_实际\_输出\_格式。 随机数字是由发送应用程序生成的，在 DXGKMDT\_OPM 的**rnRandomNumber**成员中提供，\_获取\_信息\_参数。

 

驱动程序为所指示的请求返回以下信息：

-   对于 DXGKMDT\_OPM\_获取在**guidInformation**成员中设置\_支持\_保护\_类型，**并在 DXGKMDT**\_OPM\_获取\_INFO\_参数结构中未定义，驱动程序指示可用的保护机制类型。 为了指明可用的保护类型，驱动程序将返回\_DXGKMDT 中的值的有效按位 "或" 组合[ **\_保护\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_protection_type)枚举中的**ulInformation**成员 DXGKMDT\_OPM\_标准\_信息。 DXGKMDT\_OPM\_保护\_类型\_HDCP 和 DXGKMDT\_OPM\_DPCP\_类型\_值有效。

-   对于 DXGKMDT\_OPM\_获取**guidInformation**中设置的\_连接器\_类型，并在**abParameters**中定义，驱动程序指示连接器类型。 为了指示连接器类型，驱动程序将从[**D3DKMDT\_视频\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology)中返回值的有效按位 "或" 组合，\_DXGKMDT\_OPM\_标准\_信息的**ulInformation**成员中。

-   对于 DXGKMDT\_OPM\_获取\_虚拟\_保护\_LEVEL 或 DXGKMDT\_OPM\_获取在**guidInformation**中设置\_实际\_保护\_级别，在 abParameters 中设置**保护类型，驱动**程序将在 ULINFORMATION [ **\_DXGKMDT\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)的**OPM**成员中返回一个保护级别值。 如果保护类型为 DXGKMDT\_OPM\_保护\_类型\_HDCP，则保护级别的值来自[**DXGKMDT\_OPM\_HDCP\_level**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_hdcp_protection_level)枚举。\_ 如果保护类型为 DXGKMDT\_OPM\_保护\_类型\_DPCP，则保护级别的值来自[**DXGKMDT\_OPM\_DPCP\_level**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_dpcp_protection_level)枚举。\_

    DXGKMDT\_OPM\_获取\_虚拟\_保护\_LEVEL 请求为受保护的输出返回当前设置的保护级别。 DXGKMDT\_OPM\_获取\_实际\_保护\_LEVEL 请求为与受保护的输出关联的物理连接器返回当前设置的保护级别。

-   对于 DXGKMDT\_OPM\_获取**guidInformation**中设置的\_适配器\_总线\_类型，并在**abParameters**中定义，驱动程序将标识将图形适配器连接到主板芯片的上桥的总线类型和实现。 若要确定总线的类型和实现，驱动程序将返回[**DXGKMDT\_OPM\_总线\_类型\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_bus_type_and_implementation)中的值的有效按位 "或" 组合，并在 DXGKMDT\_OPM\_标准\_信息的**ulInformation**成员中\_实现枚举。

-   对于 DXGKMDT\_OPM\_在**guidInformation**中获取\_当前\_HDCP\_SRM\_版本，并在**abParameters**中定义，驱动程序将在[**ulInformation\_DXGKMDT\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)的**OPM**成员中返回一个值，该值标识受保护的输出的当前高带宽数字内容保护（HDCP）系统 Renewability 消息（SRM）的版本号。 最小有效位（位0到15）包含 SRM 的版本编号（以小字节序格式）。 有关 SRM 版本号的详细信息，请参阅[HDCP 规范修订版本 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)。

-   对于 DXGKMDT\_OPM\_在**guidInformation**中获取\_实际\_输出\_格式，在**abParameters**中未定义，驱动程序将返回 DXGKMDT\_OPM 的成员中的信息\_[**实际\_输出\_格式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_actual_output_format)，描述如何格式化与受保护的输出关联的物理连接器的信号。

-   对于 DXGKMDT\_OPM\_获取在**guidInformation**中设置并在**abParameters**中未定义\_输出\_id，驱动程序将返回[**DXGKMDT\_OPM\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_output_id)的成员中的信息，该 id 用于标识输出连接器。\_

-   对于 DXGKMDT\_OPM\_获取**guidInformation**成员中**设置的\_** DVI\_特性，并在 DXGKMDT\_OPM\_获取\_INFO\_参数结构中未定义，驱动程序指示数字视频接口（DVI）输出连接器的电气特性。 若要指明 DVI 电气特征，驱动程序将返回 DXGKDT\_OPM 中的值之一，其中的**ulInformation**成员\_的成员中[ **\_DVI\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkdt_opm_dvi_characteristics)枚举[ **\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_standard_information)。

 

 





