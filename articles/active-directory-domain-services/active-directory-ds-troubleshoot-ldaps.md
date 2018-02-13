---
title: "Azure Active Directory 域服务：安全 LDAP 配置疑难解答 | Microsoft Docs"
description: "Azure AD 域服务的安全 LDAP 疑难解答"
services: active-directory-ds
documentationcenter: 
author: eringreenlee
manager: 
editor: 
ms.assetid: 81208c0b-8d41-4f65-be15-42119b1b5957
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2018
ms.author: ergreenl
ms.openlocfilehash: ad98f3fb1ddb753976be627764d34864e5bf3d50
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="azure-ad-domain-services---troubleshooting-secure-ldap-configuration"></a>Azure AD 域服务 - 安全 LDAP 配置疑难解答

本文提供为 Azure AD 域服务[配置安全 LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md) 时常见问题的解决方法。

## <a name="aadds101-secure-ldap-network-security-group-configuration"></a>AADDS101：安全 LDAP 网络安全组配置

**警报消息：**

已为托管域启用 Internet 上的安全 LDAP。*但是，访问端口 636 未使用网络安全组锁定。这样可能会使托管域上的用户帐户遭到密码暴力攻击。*

### <a name="secure-ldap-port"></a>安全 LDAP 端口

启用安全 LDAP 后，我们建议创建其他规则，以支持仅从特定 IP 地址的入站 LDAPS 访问。 这些规则可以使域免受可能构成安全威胁的暴力攻击。 端口 636 支持对托管域的访问。 下面介绍如何更新 NSG 以允许安全 LDAP 的访问：

1. 导航到 Azure 门户中的[“网络安全组”选项卡](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Network%2FNetworkSecurityGroups)
2. 从表中选择与域相关联的 NSG。
3. 单击“入站安全规则”
4. 创建端口 636 规则
   1. 单击顶部导航栏上的“添加”。
   2. 为源选择一个“IP 地址”。
   3. 指定此规则的源端口范围。
   4. 针对目标端口范围，输入“636”。
   5. 协议为 TCP。
   6. 为规则指定适当的名称、说明和优先级。 此规则的优先级应高于“全部拒绝”规则的优先级（如果有）。
   7. 单击“确定”。
5. 验证是否已创建规则。
6. 在两小时后检查域的运行状况，确保已正确完成相关步骤。


## <a name="contact-us"></a>联系我们
欢迎联系 Azure Active Directory 域服务产品团队[分享看法或请求支持](active-directory-ds-contact-us.md)。