---
title: Azure 中的 Linux HPC Pack 群集选项 | Microsoft Docs
description: 了解使用 Microsoft HPC Pack 在 Azure 云中创建和管理 Linux 高性能计算 (HPC) 群集时可用的选项
services: virtual-machines-linux,cloud-services
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/26/2017
ms.author: danlep
ms.openlocfilehash: 96e77b739550c935316f7bade57b8aac7e634f02
ms.sourcegitcommit: 5b2ac9e6d8539c11ab0891b686b8afa12441a8f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="options-with-hpc-pack-to-create-and-manage-a-cluster-for-linux-hpc-workloads-in-azure"></a>使用 HPC Pack 为 Azure 中的 Linux HPC 工作负荷创建和管理群集的选项
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

这篇文章重点介绍使用 HPC Pack 运行 Linux 工作负荷的选项。 还有用于运行[具有 HPC Pack 的 Windows HPC 工作负荷](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)的选项。

## <a name="hpc-pack-cluster-in-azure-vms-and-vm-scale-sets"></a>Azure VM 和 VM 规模集中的 HPC Pack 群集
### <a name="azure-templates"></a>Azure 模板
* (GitHub) [HPC Pack 2016 群集模板](https://github.com/MsHpcPack/HPCPack2016)
* (GitHub) [HPC Pack 2012 R2 群集模板](https://github.com/MsHpcPack/HPCPack2012R2)
* (Marketplace) [Linux 工作负荷的 HPC Pack 群集](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)
* （快速入门）[使用 Linux 计算节点创建 HPC 群集](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)

### <a name="powershell-deployment-script-for-hpc-pack-2012-r2"></a>适用于 HPC Pack 2012 R2 的 PowerShell 部署脚本
* [使用 HPC Pack IaaS 部署脚本创建 Linux HPC 群集](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a>教程
* [教程：Azure 的 HPC Pack 群集中的 Linux 计算节点入门](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [教程：在 Azure 中的 Linux 计算节点上使用 Microsoft HPC Pack 运行 NAMD](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [教程：在 Azure 中的 Linux RDMA 群集上运行 OpenFOAM 和 Microsoft HPC Pack](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [教程：在 Azure 中的 Linux RDMA 群集上运行 STAR-CCM+ 和 Microsoft HPC Pack](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a>群集管理
* [将作业提交到 Azure 中的 HPC Pack 群集](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [HPC Pack 中的作业管理](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="rdma-clusters-for-mpi-workloads"></a>MPI 工作负荷的 RDMA 群集
* [教程：在 Azure 中的 Linux RDMA 群集上运行 OpenFOAM 和 Microsoft HPC Pack](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [设置 Linux RDMA 群集以运行 MPI 应用程序](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

