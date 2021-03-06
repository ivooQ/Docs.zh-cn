---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: 使用 OWIN 自托管 ASP.NET Web API 2 |Microsoft Docs
author: rick-anderson
description: 本教程演示如何使用 OWIN 自托管 Web API 框架的控制台应用程序中托管 ASP.NET Web API。 打开 Web Interface for.NET (OWIN) d...
ms.author: aspnetcontent
ms.date: 07/09/2013
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9fba2774e3873d32115a14fa0c84b99466eda04f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830906"
---
<a name="use-owin-to-self-host-aspnet-web-api-2"></a>使用 OWIN 自托管 ASP.NET Web API 2
====================
通过[Kanchan Mehrotra](https://twitter.com/kanchanmeh)

> 本教程演示如何使用 OWIN 自托管 Web API 框架的控制台应用程序中托管 ASP.NET Web API。
> 
> [用于.NET 开放 Web 接口](http://owin.org)(OWIN) 定义.NET web 服务器和 web 应用程序之间的抽象。 OWIN 将从服务器中，这使 OWIN 适合于自承载在 IIS 外部自己进程中的 web 应用程序的 web 应用程序中分离出来。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) （也适用于 Visual Studio 2012）
> - Web API 2


> [!NOTE]
> 您可以在本教程中找到完整的源代码[aspnet.codeplex.com](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OwinSelfhostSample/ReadMe.txt)。


## <a name="create-a-console-application"></a>创建控制台应用程序

上**文件**菜单上，单击**新建**，然后单击**项目**。 从**已安装的模板**，在 Visual C# 中，单击**Windows** ，然后单击**控制台应用程序**。 命名项目"OwinSelfhostSample"，然后单击**确定**。

[![](use-owin-to-self-host-web-api/_static/image2.png)](use-owin-to-self-host-web-api/_static/image1.png)

## <a name="add-the-web-api-and-owin-packages"></a>添加 Web API 和 OWIN 包

从**工具**菜单上，单击**库程序包管理器**，然后单击**程序包管理器控制台**。 在包管理器控制台窗口中，输入以下命令：

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

这将安装 WebAPI OWIN selfhost 包和所有所需的 OWIN 包。

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a>配置 Web API 的自托管

在解决方案资源管理器，右键单击项目，然后选择**外** / **类**以添加一个新类。 将此类命名为 `Startup`。

![](use-owin-to-self-host-web-api/_static/image5.png)

使用以下内容替换所有样板代码，此文件中：

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a>添加 Web API 控制器

接下来，添加 Web API 控制器类。 在解决方案资源管理器，右键单击项目，然后选择**外** / **类**以添加一个新类。 将此类命名为 `ValuesController`。

使用以下内容替换所有样板代码，此文件中：

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-using-httpclient"></a>启动 OWIN 主机并发出使用 HttpClient 请求

使用以下内容替换所有 Program.cs 文件中的样板代码：

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="running-the-application"></a>运行应用程序

若要运行该应用程序，请在 Visual Studio 中按 F5。 输出应如下所示：

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a>其他资源

[项目 Katana 概述](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[承载在 Azure 辅助角色中的 ASP.NET Web API](host-aspnet-web-api-in-an-azure-worker-role.md)
