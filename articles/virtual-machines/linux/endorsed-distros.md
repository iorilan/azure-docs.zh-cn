---
title: Linux 的认可分发 | Microsoft Docs
description: 了解 Azure 认可的分发中的 Linux，包括 Ubuntu、CentOS、Oracle 和 SUSE 的指南。
services: virtual-machines-linux
documentationcenter: ''
author: szarkos
manager: jeconnoc
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2017
ms.author: szark
ms.openlocfilehash: c2233ab32314655c510c8c884641293ae3325ef5
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
---
# <a name="linux-on-distributions-endorsed-by-azure"></a>Azure 认可的分发中的 Linux
合作伙伴在 Azure Marketplace 中提供了 Linux 映像。 我们正积极与各大 Linux 社区合作，争取为认可分发列表添加更多成员。 在此期间，对于 Marketplace 未提供的分发，用户始终可以按照[创建并上传包含 Linux 操作系统的虚拟硬盘](https://docs.microsoft.com/azure/virtual-machines/linux/create-upload-generic)中的准则安装自己的 Linux。

## <a name="supported-distributions-and-versions"></a>支持的分发和版本
下表列出了 Azure 支持的 Linux 分发和版本。 有关 Azure 中支持 Linux 和开源代码技术的更多详细信息，请参阅 [Microsoft Azure 中对 Linux 映像的支持](https://support.microsoft.com/help/2941892/support-for-linux-and-open-source-technology-in-azure)。

Hyper-V 和 Azure 的 Linux 集成服务 (LIS) 驱动程序是 Microsoft 直接为上游 Linux 内核提供的内核模块。  某些 LIS 驱动程序默认内置于分发的内核中。 基于 Red Hat Enterprise (RHEL)/CentOS 的早期分发在[用于 Hyper-V 和 Azure 的 Linux Integration Services 版本 4.2](https://www.microsoft.com/en-us/download/details.aspx?id=55106) 以单独下载的形式提供。 有关 LIS 驱动程序的详细信息，请参阅 [Linux 内核要求](create-upload-generic.md#linux-kernel-requirements)。

Azure Linux 代理已预安装在 Azure Marketplace 映像中，通常可从分发的包存储库中获得。 源代码可在 [GitHub](https://github.com/azure/walinuxagent) 上找到。

  
| 分发 | 版本 | 驱动程序 | 代理 |
| --- | --- | --- | --- |
| CentOS |CentOS 6.3+、7.0+ |CentOS 6.3：[LIS 下载](https://www.microsoft.com/en-us/download/details.aspx?id=55106)<p>CentOS 6.4+：在内核中 |包：在“WALinuxAgent”下的[存储库](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/)中 <br/>源代码：[GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0+ |在内核中 |源代码：[GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7.9+、8.2+ |在内核中 |包：在“waagent”下的存储库中 <br/>源代码：[GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4+、7.0+ |在内核中 |包：在“WALinuxAgent”下的存储库中 <br/>源代码：[GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux |RHEL 6.7+、7.1+ |在内核中 |包：在“WALinuxAgent”下的存储库中 <br/>源代码：[GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES/SLES for SAP<br>11 SP4<br>12 SP1+|在内核中 |包：<p> 对于 11，在 [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools) 存储库中<br>对于 12，包含在“公有云”模块中的“python-azure-agent”下<br/>源代码：[GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE Leap 42.2+ |在内核中 |包：在“python-azure-agent”下的 [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools) 存储库中 <br/>源代码：[GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04+ **<sup>1</sup>** |在内核中 |包：在“walinuxagent”下的存储库中 <br/>源代码：[GitHub](https://github.com/Azure/WALinuxAgent) |

  - **<sup>1</sup>** 有关在 Azure 中对 Ubuntu 12.04 的支持，请参阅 [EOL 通知](https://azure.microsoft.com/blog/ubuntu-12-04-precise-pangolin-nearing-end-of-life/)。


## <a name="partners"></a>合作伙伴

### <a name="coreos"></a>CoreOS
[https://coreos.com/docs/running-coreos/cloud-providers/azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

从 CoreOS 网站：

*CoreOS 在设计时就已考虑到了安全性、一致性和可靠性。CoreOS 使用 Linux 容器在更高的抽象级别管理服务，而不是通过 yum 或 apt 来安装程序包。单个服务的代码和所有依赖项都打包在一个容器中，这个容器可以运行在一个或多个 CoreOS 计算机中。*

### <a name="credativ"></a>Credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ 是一家独立的咨询和服务公司，致力于使用免费软件开发和实施专业解决方案。 Credativ 是获得国际认可的开源领域专业先行者，为许多公司的 IT 部门提供支持。 Credativ 与 Microsoft 合作，目前正在为 Debian 8 (Jessie) 以及 Debian 7 (Wheezy) 之前的版本准备相应的 Debian 映像。 这些映像经过专门的设计，可以在 Azure 上运行并通过该平台轻松进行管理。 Credativ 还会通过其开源支持中心为 Azure 的 Debian 映像的维护和更新提供长期支持。

### <a name="oracle"></a>Oracle
[http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

Oracle 的策略是为公有云和私有云提供广泛的解决方案， 让客户面临如何在 Oracle 云以及其他云中部署 Oracle 软件这一问题时拥有更多选择权和灵活性。 通过 Oracle 与 Microsoft 的合作关系，客户可以凭借可信的证书和 Oracle 支持在 Microsoft 公有和私有云中部署 Oracle 软件。  Oracle 对 Oracle 公有和私有云的承诺和投资保持不变。

### <a name="red-hat"></a>Red Hat
[http://www.redhat.com/en/partners/strategic-alliance/microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

作为世界上领先的开源解决方案提供商，Red Hat 帮助 90% 以上的财富 500 强公司解决业务难题、调整 IT 与业务策略，以及为未来技术做准备。 Red Hat 通过开放式业务模型和价格合理、可预测的订阅模型提供安全的解决方案，从而实现了此目的。

### <a name="suse"></a>SUSE
[http://www.suse.com/suse-linux-enterprise-server-on-azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

Azure 上的 SUSE Linux Enterprise Server 是一个已验证的平台，该平台为云计算提供了高级可靠性和安全性。 SUSE 的通用 Linux 平台可与 Azure 云服务无缝集成，以便交付易于管理的云环境。 借助 1,800 多个独立软件供应商提供的适用于 SUSE Linux Enterprise Server 的 9,200 多个认证应用程序，SUSE 可确保满怀信心地在 Azure 上部署数据中心内支持的运行工作负荷。

### <a name="canonical"></a>Canonical
[http://www.ubuntu.com/cloud/azure](http://www.ubuntu.com/cloud/azure)

Canonical 工程和开放社区监管对 Ubuntu 在客户端、服务器和云计算（包括用户的个人云服务）方面获得成功起到了推动作用。 Canonical 期望使用 Ubuntu 开发一个统一的免费平台（从手机到云），该平台带有一系列适用于手机、平板电脑、TV 和桌面的相关接口， 从而使 Ubuntu 成为各种机构（从公有云提供商到消费类电子产品制造商）的首选以及各个技术专家的最爱。

借助遍布全球的开发人员和工程中心这一独特优势，Canonical 将与硬件制造商、内容提供商和软件开发人员通力合作，将 Ubuntu 解决方案推向 PC、服务器和手持设备市场。
