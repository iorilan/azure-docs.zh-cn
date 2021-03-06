---
title: include 文件
description: include 文件
services: data-factory
author: linda33wj
ms.service: data-factory
ms.topic: include
ms.date: 05/16/2018
ms.author: jingwang
ms.custom: include file
ms.openlocfilehash: 63653795ad8c52e2743fb02fa804dd2edbf0d2ab
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2018
---
数据工厂是一项多租户服务，具有以下默认限制，目的是确保客户订阅不受彼此工作负荷的影响。 订阅的许多限制只需联系支持部门即可提高，最多可提高到最大限制。

### <a name="version-2"></a>版本 2

| 资源 | 默认限制 | 最大限制 | 
| -------- | ------------- | ------------- | 
| Azure 订阅中的数据工厂 | 50 | [联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 数据工厂中的管道 | 2500 | [联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 数据工厂中的数据集 | 2500 | [联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 数据工厂中的触发器 | 2500 | [联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 数据工厂中的关联服务 | 2500 | [联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 数据工厂中的集成运行时 <sup>4</sup> | 2500 | [联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 一个订阅中 Azure-SSIS 集成运行时的总 CPU 内核数 | 100 | [联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 每个管道的并行管道运行 | 100 | [联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 每个管道的最大活动数 | 20 | 40 |
| 每个管道的最大参数个数 | 20 | 30 |
| 管道对象的每个对象字节数 <sup>1</sup> | 200 KB | 200 KB |
| 数据集和关联服务对象的每个对象字节数 <sup>1</sup> | 100 KB | 2000 KB |
| 每个活动运行的云数据移动单位 <sup>3</sup> | 256 | [联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 管道活动运行的重试次数 | 1 天（超时） | 1 天（超时） |
| 编写 API 调用 | 2500/小时<br/><br/> 此限制是由 Azure 资源管理器而不是 Azure 数据工厂所强加的。 | 请[联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)。 |
| 读取 API 调用 | 12,500/小时<br/><br/> 此限制是由 Azure 资源管理器而不是 Azure 数据工厂所强加的。 | [联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |


### <a name="version-1"></a>版本 1

| **资源** | **默认限制** | **最大限制** |
| --- | --- | --- |
| Azure 订阅中的数据工厂 |50 |[联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 数据工厂中的管道 |2500 |[联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 数据工厂中的数据集 |5000 |[联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 每个数据集的并发切片数 |10 |10 |
| 管道对象的每个对象字节数 <sup>1</sup> |200 KB |200 KB |
| 数据集和关联服务对象的每个对象字节数 <sup>1</sup> |100 KB |2000 KB |
| 订阅中的 HDInsight 按需群集核心数 <sup>2</sup> |60 |[联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 每个活动运行的云数据移动单位 <sup>3</sup> |32 |[联系支持人员](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| 管道活动运行的重试次数 |1000 |MaxInt（32 位） |

<sup>1</sup> 管道、数据集和链接服务对象代表工作负荷的逻辑组。 对这些对象的限制与可以使用 Azure 数据工厂服务移动或处理的数据量无关。 可以缩放数据工厂以处理 PB 量级的数据。

<sup>2</sup> 按需 HDInsight 核心数从包含数据工厂的订阅中分配。 因此，上述限制是数据工厂针对按需 HDInsight 核心强制实施的核心限制，不同于与 Azure 订阅关联的核心限制。

<sup>3</sup> 云数据移动单位 (DMU) 用于云到云复制操作。 它是一种度量单位，代表单个单位在数据工厂中的能力（包含 CPU、内存、网络资源分配）。 就某些方案来说，使用更多 DMU 可以提高复制吞吐量。 请参阅[云数据移动单位 (V2)](../articles/data-factory/copy-activity-performance.md#cloud-data-movement-units) 和[云数据移动单位 (V1)](../articles/data-factory/v1/data-factory-copy-activity-performance.md#cloud-data-movement-units)部分，了解详细信息。

<sup>4</sup> 集成运行时 (IR) 是 Azure 数据工厂用于在不同的网络环境之间提供以下数据集成功能的计算基础结构：数据移动、调度活动来计算服务，SSIS 包的执行。 有关详细信息，请参阅[集成运行时概述](../articles/data-factory/concepts-integration-runtime.md)。

| **资源** | **默认下限** | **最小限制** |
| --- | --- | --- |
| 计划间隔 |15 分钟 |15 分钟 |
| 重试尝试之间的间隔 |1 秒 |1 秒 |
| 重试超时值 |1 秒 |1 秒 |

#### <a name="web-service-call-limits"></a>Web 服务调用限制
Azure 资源管理器限制 API 调用。 可以根据 [Azure 资源管理器 API 限制](../articles/azure-subscription-service-limits.md#resource-group-limits)中规定的频率执行 API 调用。
