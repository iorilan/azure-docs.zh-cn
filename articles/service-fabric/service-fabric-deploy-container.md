---
title: "Service Fabric 和部署容器 | Microsoft 文档"
description: "介绍 Service Fabric，以及如何使用容器部署微服务应用程序。 本文介绍 Service Fabric 为容器提供的功能，以及如何在群集中部署 Windows 容器映像。"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/24/2016
ms.author: mfussell
translationtype: Human Translation
ms.sourcegitcommit: af9f761179896a1acdde8e8b20476b7db33ca772
ms.openlocfilehash: 1c5f3bc66c902c3b7186cad44728fa5237dd298a


---
# <a name="preview-deploy-a-windows-container-to-service-fabric"></a>预览：将 Windows 容器部署到 Service Fabric
> [!div class="op_single_selector"]
> * [部署 Windows 容器](service-fabric-deploy-container.md)
> * [部署 Docker 容器](service-fabric-deploy-container-linux.md)
> 
> 

本文将指导完成在 Windows 容器中构建容器化服务的过程。

> [!NOTE]
> 此功能在 Linux 上以预览版提供，在 Windows Server 2016 上（尚）不可用。 此功能将在即将发布的 Azure Service Fabric 版本中以预览版向 Windows Server 2016 提供。 
> 
> 

Service Fabric 提供多种容器功能，可帮助你构建由容器化的微服务组成的应用程序。 

功能包括：

* 容器映像部署和激活
* 资源调控
* 存储库身份验证
* 容器端口到主机端口映射
* 容器到容器的发现和通信
* 能够配置和设置环境变量

让我们了解将容器化服务打包到应用程序时各个功能如何发挥作用。

## <a name="package-a-windows-container"></a>打包 Windows 容器
打包容器时，可以选择使用 Visual Studio 项目模板，或者[手动创建应用程序包](#manually)。 使用 Visual Studio 时，新的项目模板将创建应用程序包结构和清单文件。 VS 模板将在以后的版本中发布。

## <a name="use-visual-studio-to-package-an-existing-container-image"></a>使用 Visual Studio 打包现有容器映像
> [!NOTE]
> 在即将发布的适用于 Service Fabric 的 Visual Studio 版本中，可以将容器添加到应用程序，其方法与现在添加来宾可执行文件的方法相同。 有关详细信息，请参阅[将来宾可执行文件部署到 Service Fabric](service-fabric-deploy-existing-app.md) 主题。 目前必须按照下节中的说明手动打包容器。
> 
> 

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container"></a>手动打包和部署容器
手动打包容器化服务的过程基于以下步骤进行：

1. 将容器发布到存储库。
2. 创建包目录结构。
3. 编辑服务清单文件。
4. 编辑应用程序清单文件。

## <a name="deploy-and-activate-a-container-image"></a>部署和激活容器映像
在 Service Fabric [应用程序模型](service-fabric-application-model.md)中，容器表示放置多个服务副本的应用程序主机。 若要部署和激活某个容器，请在服务清单的 `ContainerHost` 元素中输入容器映像的名称。

在服务清单中，为入口点添加 `ContainerHost`。 然后将 `ImageName` 设置为容器存储库和映像的名称。 下面的不完整清单演示如何从名为 `myrepo` 的存储库部署名为 `myimage:v1` 的容器：

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

可以指定含有逗号分隔命令集的可选 `Commands` 元素在容器内部运行，来提供输入命令。

## <a name="understand-resource-governance"></a>了解资源监管
资源监管是一项容器功能，其限制容器可在主机上使用的资源。 在应用程序清单中指定的 `ResourceGovernancePolicy` 用于声明服务代码包的资源限制。 可以为以下资源设置资源限制：

* 内存
* MemorySwap
* CpuShares（CPU 相对权重）
* MemoryReservationInMB  
* BlkioWeight（BlockIO 相对权重）

> [!NOTE]
> 在以后版本中，将包含对指定特定块 IO 限制（例如 IOP、读/写 BPS）和其他的支持。
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a>对存储库进行身份验证
若要下载容器，必须向容器存储库提供登录凭据。 应用程序清单中指定的登录凭据用于指定从映像存储库下载容器映像所需的登录信息或 SSH 密钥。 以下示例显示名为 *TestUser* 的帐户以及明文密码（*不*建议使用）：

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

建议使用已部署到计算机的证书加密密码。

以下示例显示名为 *TestUser* 的帐户，其密码已使用名为 *MyCert* 的证书加密。 可以使用 `Invoke-ServiceFabricEncryptText` PowerShell 命令创建密码的机密加密文本。 有关详细信息，请参阅文章[管理 Service Fabric 应用程序中的密钥](service-fabric-application-secret-management.md)。

用于解密密码的证书私钥必须使用带外方法部署到本地计算机。 （在 Azure 中该方法是 Azure Resource Manager）然后当 Service Fabric 将服务包部署到计算机时，可解密密钥。 通过使用密钥和帐户名，则可对容器存储库进行身份验证。

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping"></a>配置容器端口到主机端口映射
可以在应用程序清单中指定 `PortBinding`，设置用来与容器通信的主机端口。 端口绑定可将服务在容器中侦听的端口映射到主机上的端口。

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a>配置容器到容器的发现和通信
通过使用 `PortBinding` 策略将容器端口映射到服务清单中的 `Endpoint`，如以下示例中所示。 终结点 `Endpoint1` 可以指定固定端口（例如端口 80）。 也可不指定任何端口，在此情况下，将从群集的应用程序端口范围内选择一个随机端口。

如果在来宾容器的服务清单中使用 `Endpoint` 标记指定了终结点，则 Service Fabric 可以自动将此终结点发布到命名服务。 因此群集中运行的其他服务可以使用 REST 查询进行解析来发现该容器。

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

在命名服务中注册后，可以轻松地在容器中的代码内使用[反向代理](service-fabric-reverseproxy.md)来执行容器到容器的通信。 将 http 侦听端口和想要与其通信的服务名称作为环境变量提供给反向代理，以此方式执行通信。 有关详细信息，请参阅后续部分。 

## <a name="configure-and-set-environment-variables"></a>配置和设置环境变量
对于部署在容器中的服务，或者部署为进程/来宾可执行文件的服务，可以在服务清单中为每个代码包指定环境变量。 可以在应用程序清单中明确重写这些环境变量的值，或者在部署期间将其指定为应用程序参数。

以下服务清单 XML 代码片段演示如何指定代码包的环境变量：

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

可在应用程序清单级别重写这些环境变量：

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

在前面示例中，我们为 `HttpGateway` 环境变量指定了显式值 (19000)，`BackendServiceName` 参数的值是通过 `[BackendSvc]` 应用程序参数设置的。 通过这些设置可以在部署应用程序时指定 `BackendServiceName` 的值，而无需在清单中使用固定值。

## <a name="complete-examples-for-application-and-service-manifest"></a>应用程序清单和服务清单的完整示例

下面是应用程序清单示例：

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

下面是服务清单示例（在前面的应用程序清单中指定）：

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" Port="80"  UriScheme="http" />
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a>后续步骤
现在已部署了容器化服务，请通过阅读 [Service Fabric 应用程序生命周期](service-fabric-application-lifecycle.md)了解如何管理其生命周期。




<!--HONumber=Nov16_HO3-->

