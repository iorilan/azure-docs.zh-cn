---
title: "在 OMS 门户中跟踪 B2B 消息 | Microsoft Docs"
description: "如何在 OMS 门户中跟踪 B2B 消息"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2016
ms.author: padmavc
translationtype: Human Translation
ms.sourcegitcommit: 53195091ac4b93ed94f432990c84c407615fc03e
ms.openlocfilehash: 9c3855c7fce5a9f38424f0bb6cd03f7a2c8d36be


---
# <a name="tracking-b2b-messages-in-oms-portal"></a>在 OMS 门户中跟踪 B2B 消息
B2B 通信涉及到两个正在运行的业务流程或应用程序之间的消息交换。 在 OMS 门户中跟踪 B2B 消息，可获得基于 Web 的丰富跟踪功能，能够查看消息是否已正确处理。  可跟踪

* 计数和消息状态
* 确认状态
* 已确认的关联消息
* 有关故障的详细错误说明
* 搜索功能

## <a name="prerequisites"></a>先决条件
* Azure 帐户；可以创建[免费帐户](https://azure.microsoft.com/free)
* 集成帐户；可创建[集成帐户](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)并启用日志记录；可在[此处](logic-apps-monitor-b2b-message.md)找到步骤
* 逻辑应用；可创建[逻辑应用](../logic-apps/logic-apps-create-a-logic-app.md)并启用日志记录；可在[此处](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics-and-alerts)找到步骤

## <a name="adding-logic-apps-b2b-solution-to-oms-portal"></a>将逻辑应用 B2B 解决方案添加到 OMS 门户

1. 在门户中选择“更多服务”，搜索 **log analytics** 并选择“Log Analytics”   
![搜索 Log Analytics](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)  

2. 选择“Log Analytics”  
![选择 Log Analytics](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. 选择“OMS 门户”，打开 OMS 门户主页   
![浏览 OMS 门户](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. 选择“解决方案库”    
![选择解决方案库](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. 选择“逻辑应用 B2B”     
![选择逻辑应用 B2B](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. 单击“添加”，将“逻辑应用 B2B 消息”添加到主页  
![选择添加](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

7. 浏览主页，查看“逻辑应用 B2B 消息”   
![选择主页](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

## <a name="tracking-data-in-oms-portal"></a>在 OMS 门户中跟踪数据

1. 发布消息过程；主页更新消息计数   
![选择主页](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

2. 在主页上选择“逻辑应用 B2B 消息”，显示 AS2 和 X12 消息状态。  数据以最后一天为基础。
![选择逻辑应用 B2B 消息](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)



3. 按状态选择 AS2 或 X12 消息会转到消息列表   
![选择 AS2 消息状态](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

| 属性 | 说明 |
| --- | --- |
| 发送方 | 接收设置中配置的来宾合作伙伴或发送设置中配置的托管合作伙伴发送 AS2 协议的设置 |
| 接收方 | 接收设置中配置的托管合作伙伴或发送设置中配置的来宾合作伙伴发送 AS2 协议的设置 |
| 逻辑应用 | 配置了 AS2 操作的逻辑应用 |
| 状态 | AS2 消息状态。 Success = 已接收或发送正常的 AS2 消息，未配置 MDN；Success = 已接收或发送正常的 AS2 消息，已配置 MDN 并且已接收或发送 MDN；Failed = 已接收错误的 AS2 消息，未配置 MDN；Pending = 已接收或发送正常的 AS2 消息，已配置 MDN，预期会收到功能确认。 |
| Ack | MDN 消息状态 |
| Direction | AS2 消息方向 |
| 相关性 ID | 用于关联逻辑应用中所有触发器和操作的 ID |
| 消息 ID |  AS2 消息 ID，来自 AS2 消息的标头 |
| Timestamp | AS2 操作处理消息的时间 |
|  |  |


![选择 X12 消息状态](media/logic-apps-track-b2b-messages-omsportal/x12messagelist.png)

| 属性 | 说明 |
| --- | --- |
| 发送方 | 接收设置中配置的来宾合作伙伴或发送设置中配置的托管合作伙伴发送 AS2 协议的设置 |
| 接收方 | 接收设置中配置的托管合作伙伴或发送设置中配置的来宾合作伙伴发送 AS2 协议的设置 |
| 逻辑应用 | 配置了 AS2 操作的逻辑应用 |
| 状态 | X12 消息状态。 Success = 已接收或发送正常的 X12 消息，未配置功能确认；Success = 已接收或发送正常的 X12 消息，已配置功能确认并且已接收或发送功能确认；Failed = 已接收或发送错误的 X12 消息，未配置功能确认；Pending = 已接收或发送正常的 X12 消息，已配置功能确认，预期会收到功能确认 |
| Ack | 功能确认 (997) 状态。  Accepted = 已接收或发送正面功能确认；Rejected = 已接收或发送负面功能确认；Pending = 预期会收到功能确认，但未收到；Pending = 生成了功能确认，但无法将它发送给合作伙伴 |
| Direction | X12 消息方向 |
| 相关性 ID | 用于关联逻辑应用中所有触发器和操作的 ID |
| 消息类型 |  EDI X12 消息类型 |
| ICN | X12 消息的交换控制编号 |
| TSCN | X12 消息的事务集控制编号 |
| Timestamp | X12 操作处理消息的时间 |
| | |

4. 选择 AS2 或 X12 消息列表中的某行会转到日志搜索。  日志搜索列出具有相同**运行 ID** 的所有操作
![选择消息状态](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

## <a name="queries-in-oms-portal"></a>OMS 门户中的查询

可在“搜索”页上创建查询，然后在搜索时使用 Facet 控件筛选结果。

### <a name="how-to-create-a-query"></a>如何创建查询

1. 在日志搜索中，编写查询并选择“保存”。  [此处](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)提供编写查询的步骤![选择主页](media/logic-apps-track-b2b-messages-omsportal/logsearchaddquery.png)

2. 将打开“保存搜索”。  提供**名称**、**类别**，并单击“保存”   
![选择主页](media/logic-apps-track-b2b-messages-omsportal/logsearchaddquery1.png)

3. 若要查看查询，请选择“收藏夹”    
![选择主页](media/logic-apps-track-b2b-messages-omsportal/logsearchaddquery3.png)

    ![选择主页](media/logic-apps-track-b2b-messages-omsportal/logsearchaddquery4.png)

### <a name="how-to-use-a-saved-query"></a>如何使用已保存的查询

* 在日志搜索中，选择“收藏夹”，查看已保存的查询。  选择其中一个查询提供查询结果![选择主页](media/logic-apps-track-b2b-messages-omsportal/logsearchaddquery5.png)


## <a name="next-steps"></a>后续步骤
[自定义跟踪架构](logic-apps-track-integration-account-custom-tracking-schema.md "Learn about Custom Tracking Schema")   
[AS2 跟踪架构](logic-apps-track-integration-account-as2-tracking-schemas.md "Learn about AS2 Tracking Schema")    
[X12 跟踪架构](logic-apps-track-integration-account-x12-tracking-schema.md "Learn about X12 Tracking Schema")  
[了解有关 Enterprise Integration Pack 的详细信息](../logic-apps/logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack") 


<!--HONumber=Jan17_HO4-->

