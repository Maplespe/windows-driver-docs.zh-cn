---
title: 辅助安装程序操作
description: 辅助安装程序操作
ms.assetid: a7f52125-b435-4963-85dc-712700ba9fe9
keywords:
- 共同安装程序的 WDK 设备安装，其工作原理
- 共同安装程序 WDK 设备安装，示例
- SetupDiCallClassInstaller
- 类共同安装程序 WDK
- DIF 请求共同安装程序示例 WDK
- 设备特定的共同安装程序 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad7fba0e2ade733f3d696c08029150e8fe91e799
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840657"
---
# <a name="co-installer-operation"></a>辅助安装程序操作





Setupapi.log 调用共同安装程序，如下图所示。

![阐释共同安装程序如何参与设备安装的关系图](images/coinsts.png)

Unshaded 框表示操作系统为[系统提供的设备安装程序类](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))提供的组件。 着色框表示您可以提供的组件。 如果创建自定义设备安装程序类，还可以提供类安装程序。 但是，很少需要创建新的设备安装程序类，因为几乎每个设备都可以与系统提供的设备安装程序类之一相关联。 有关 Windows 组件的详细信息，请参阅[设备安装概述](overview-of-device-and-driver-installation.md)。

可以为特定设备（*设备特定的共同安装程序*）或设备安装程序类（*类共同安装*程序）提供共同安装程序。 仅当安装为其注册了共同安装程序的设备时，Setupapi.log 才会调用设备特定的共同安装程序。 操作系统和供应商可以为设备注册零个或多个特定于设备的共同安装程序。 当安装为其注册了共同安装程序的设备安装程序类的任何设备时，Setupapi.log 会调用类共同安装程序。 操作系统和供应商可以为设备安装程序类注册一个或多个类共同安装程序。 此外，可以为一个或多个安装程序类注册类共同安装程序。

Windows 和[自定义设备安装应用程序](writing-a-device-installation-application.md)通过使用[设备安装函数代码](https://docs.microsoft.com/previous-versions/ff541307(v=vs.85))（DIF 代码）调用[**SetupDiCallClassInstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)来安装设备。

在 GUI 模式安装过程中，操作系统通过 DIF 代码调用[**SetupDiCallClassInstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller) ，以检测系统中存在的非 PnP 设备。 IHV 通常会提供共同安装程序，为 IHV 发布的非 PnP 设备执行此操作。

对于每个 DIF 请求， **SetupDiCallClassInstaller**会调用注册到设备的安装程序类的任何类共同安装程序、为特定设备注册的任何设备共同安装程序，以及系统为设备提供的类安装程序的安装程序类（如果有）。

自定义设备安装应用程序必须调用**SetupDiCallClassInstaller** ，而不是直接调用共同安装程序或类安装程序。 此函数可确保正确调用所有注册的共同安装程序。

类共同安装程序通常在安装设备之前注册，设备特定的共同安装程序将注册为设备安装的一部分。 因此，在设备安装过程中，类共同安装程序通常会被添加到共同安装程序列表，并为所有 DIF 请求调用。

为设备（或已调用[**SetupDiRegisterCoDeviceInstallers**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers) ）完成[**DIF_REGISTER_COINSTALLERS**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-register-coinstallers)请求后，操作系统会将特定于设备的共同安装程序添加到共同安装程序列表中。 设备特定的共同安装程序不参与以下 DIF 请求：

[**DIF_ALLOW_INSTALL**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-allow-install)

[**DIF_INSTALLDEVICEFILES**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevicefiles)

[**DIF_SELECTBESTCOMPATDRV**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-selectbestcompatdrv)

只有类共同安装程序（而不是设备特定的共同安装程序）才能响应以下 DIF 请求：

[**DIF_DETECT**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-detect)

[**DIF_FIRSTTIMESETUP**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-firsttimesetup)

[**DIF_NEWDEVICEWIZARD_PRESELECT**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-preselect)

[**DIF_NEWDEVICEWIZARD_SELECT**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-select)

[**DIF_NEWDEVICEWIZARD_PREANALYZE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-preanalyze)

[**DIF_NEWDEVICEWIZARD_POSTANALYZE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-postanalyze)

在这些上下文中，设备共同安装程序并不适用，这是因为尚未标识特定设备或在此早期安装阶段，或者尚未注册设备共同安装程序。

下图显示了在注册了任何特定于设备的共同安装程序后， **SetupDiCallClassInstaller**调用共同安装程序和类安装程序的顺序。

![为 dif 请求处理和后处理调用共同安装程序的示意图](images/callco.png)

在上图所示的示例中，为此设备的安装程序类注册了两个类共同安装程序，并为该设备注册了一个特定于设备的共同安装程序。 以下步骤与上图中的带圆圈数字相对应：

1.  **SetupDiCallClassInstaller**调用第一个类共同安装程序，指定一个用于指示正在处理的安装请求的 DIF 代码（在本示例中为[**DIF_INSTALLDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevice)）。 共同安装程序可以选择参与安装请求。 在此示例中，第一个注册的类共同安装程序返回 NO_ERROR。

2.  反过来， **SetupDiCallClassInstaller**调用任何其他注册的类共同安装程序。 在此示例中，第二个类共同安装程序返回 ERROR_DI_POSTPROCESSING_REQUIRED，这会要求稍后调用共同安装程序进行后处理。

3.  **SetupDiCallClassInstaller**将调用任何注册的设备特定的共同安装程序。

4.  在调用了所有已注册的共同安装程序后， **SetupDiCallClassInstaller**将调用系统提供的类安装程序（如果设备的安装程序类有一个安装程序）。 在此示例中，类安装程序返回 ERROR_DI_DO_DEFAULT，这是类安装程序的典型返回值。

5.  **SetupDiCallClassInstaller**调用安装请求的默认处理程序（如果有）。 DIF_INSTALLDEVICE 具有默认处理程序[**SetupDiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)，它是 setupapi.log 的一部分。

6.  **SetupDiCallClassInstaller**调用请求后处理的所有共同安装程序。 在此示例中，第二个类共同安装程序请求了后处理。

共同安装程序的后处理类似于 driver [**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，只是在它的单个入口点调用了共同安装程序。 当**SetupDiCallClassInstaller**调用共同安装程序进行后处理时，它会将*后处理*设置为**TRUE** ，并将*InstallResult*设置为*上下文*参数中的相应值。 在此示例中为*上下文*。*InstallResult*是 NO_ERROR 的，因为默认处理程序已成功执行。

对于后处理， **SetupDiCallClassInstaller**以相反顺序调用共同安装程序。 如果上图中的所有共同安装程序都已返回 ERROR_DI_POSTPROCESSING_REQUIRED，则**SetupDiCallClassInstaller**将先调用 Device_Coinstaller_1 进行后处理，然后再执行 Class_Coinstaller_2，然后 Class_Coinstaller_1。 类安装程序不请求后处理;仅限共同安装程序。

即使之前的共同安装程序未能安装请求，也会调用请求后处理的共同安装程序。

 

 





