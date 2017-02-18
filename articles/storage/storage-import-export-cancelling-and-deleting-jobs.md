---
title: "取消和删除 Azure 导入/导出服务作业 | Microsoft Docs"
description: "了解如何取消和删除 Microsoft Azure 导入/导出服务的作业"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/01/2017
ms.author: muralikk
translationtype: Human Translation
ms.sourcegitcommit: 22e37e26fec913a7638c71b2547c38f5efacd10b
ms.openlocfilehash: 640b814e4280f5cce029bea7324881bbfef4b1a4


---

# <a name="cancelling-and-deleting-jobs"></a>取消和删除作业
在作业进入 `Packaging` 状态之前，可以通过调用[更新作业属性](/rest/api/storageimportexport/jobs#Jobs_Update)操作并将 `CancelRequested` 元素设置为 `true` 来请求取消该作业。 系统会尽最大努力取消该作业。 如果驱动器正在传输数据，则即使在请求取消后，数据也仍可能继续传输。

 已取消的作业将转换为 `Completed` 状态并保留 90 天，之后将被删除。

 若要删除某个作业，请在传送该作业之前（*即*，在该作业处于 `Creating` 状态时）调用[删除作业](/rest/api/storageimportexport/jobs#Jobs_Delete)操作。 也可以在作业处于 `Completed` 状态时将其删除。 删除某个作业后，不再能够通过 REST API 或 Azure 门户访问其信息和状态。

## <a name="see-also"></a>另请参阅
 [使用导入/导出服务 REST API](storage-import-export-using-the-rest-api.md)



<!--HONumber=Dec16_HO3-->

