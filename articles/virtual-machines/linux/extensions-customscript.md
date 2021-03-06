---
title: 在 Azure 中的 Linux VM 上运行自定义脚本 | Microsoft 文档
description: 使用自定义脚本扩展自动化 Linux VM 配置任务
services: virtual-machines-linux
documentationcenter: ''
author: danielsollondon
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: danis
ms.openlocfilehash: 88f337df14b7e2647a76cce7ef91ec6f8950bbc6
ms.sourcegitcommit: 5b2ac9e6d8539c11ab0891b686b8afa12441a8f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="use-the-azure-custom-script-extension-with-linux-virtual-machines"></a>在 Linux 虚拟机上使用 Azure 自定义脚本扩展
自定义脚本扩展在 Azure 虚拟机上下载和运行脚本。 此扩展适用于部署后配置、软件安装或其他任何配置/管理任务。 可以从 Azure 存储或其他可访问的 Internet 位置下载脚本，或者将脚本提供给扩展运行时。 

将自定义脚本扩展与 Azure 资源管理器模板集成。 也可使用 Azure CLI、PowerShell、Azure 门户或 Azure 虚拟机 REST API 来运行它。

本文详细介绍如何使用 Azure CLI 中的自定义脚本扩展以及如何使用 Azure 资源管理器模板运行扩展。 本文还提供针对 Linux 系统的疑难解答步骤。

## <a name="extension-configuration"></a>扩展配置
自定义脚本扩展配置指定脚本位置和要运行命令等设置。 可将此配置存储在配置文件中、在命令行中指定，或者在 Azure 资源管理器模板中指定该配置。 

可将敏感数据存储在受保护的配置中，此配置经过加密，只能在虚拟机内部解密。 当执行命令包含机密（例如密码）时，受保护的配置相当有用。

### <a name="public-configuration"></a>公共配置
公共配置的架构如下所示。

>[!NOTE]
>这些属性名称区分大小写。 要避免部署问题，请使用如下所示的名称。

* **commandToExecute**（必需，字符串）：要运行的入口点脚本。
* **fileUris**（可选，字符串数组）：要下载的文件的 URL。
* **timestamp**（可选，整数）：脚本的时间戳。 仅当要触发脚本的重新运行操作时才可更改此字段的值。

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>受保护的配置
受保护的配置的架构如下所示。

>[!NOTE]
>这些属性名称区分大小写。 要避免部署问题，请使用如下所示的名称。

* **commandToExecute**（可选，字符串）：要运行的入口点脚本。 如果命令包含机密（例如密码），请使用此字段。
* **storageAccountName**（可选，字符串）：存储帐户的名称。 如果指定存储凭据，所有文件 URI 必须是 Azure Blob 的 URL。
* **storageAccountKey**（可选，字符串）：存储帐户的访问密钥。

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>Azure CLI
在使用 Azure CLI 运行自定义脚本扩展时，请创建一个或多个配置文件。 配置文件至少要包含文件 URI 和脚本执行命令。

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

（可选）可以在命令中以 JSON 格式字符串的形式指定设置。 这样，便可以在执行期间指定配置，而无需使用单独的配置文件。

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"],"commandToExecute": "./config-music.sh"}'
```

### <a name="azure-cli-examples"></a>Azure CLI 示例

#### <a name="public-configuration-with-script-file"></a>包含脚本文件的公共配置

```json
{
  "fileUris": ["https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"],
  "commandToExecute": "./config-music.sh"
}
```

Azure CLI 命令：

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

#### <a name="public-configuration-with-no-script-file"></a>不包含脚本文件的公共配置

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

Azure CLI 命令：

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

#### <a name="public-and-protected-configuration-files"></a>公共和受保护的配置文件

使用公共配置文件来指定脚本文件 URI。 使用受保护的配置文件来指定要运行的命令。

公共配置文件：

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

受保护的配置文件：  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

Azure CLI 命令：

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a>资源管理器模板
可使用资源管理器模板在虚拟机部署时运行 Azure 自定义脚本扩展。 为此，请将格式正确的 JSON 添加到部署模板。

### <a name="resource-manager-examples"></a>资源管理器示例

#### <a name="public-configuration"></a>公共配置

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

#### <a name="execution-command-in-protected-configuration"></a>受保护配置中的执行命令

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

有关完整示例，请参阅 [.NET Music 商店演示](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)。

## <a name="troubleshooting"></a>故障排除
运行自定义脚本扩展时，会创建脚本，或将脚本下载到类似于以下示例的目录中。 命令输出也会保存到此目录中的 `stdout` 和 `stderr` 文件中。

```bash
/var/lib/waagent/custom-script/download/0/
```

Azure 脚本扩展生成一个日志，位置如下：

```bash
/var/log/azure/custom-script/handler.log
```

也可使用 Azure CLI 来检索自定义脚本扩展的执行状态：

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

输出类似于以下文本：

```azurecli
info:    Executing command vm extension get
+ Looking up the VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>后续步骤
有关其他 VM 脚本扩展的信息，请参阅[适用于 Linux 的 Azure 脚本扩展概述](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

