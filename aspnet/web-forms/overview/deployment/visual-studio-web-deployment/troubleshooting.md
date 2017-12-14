---
uid: web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
title: "使用 Visual Studio 的 ASP.NET Web 部署： 故障排除 |Microsoft 文档"
author: tdykstra
description: "本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，使用的..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/01/2015
ms.topic: article
ms.assetid: c0090595-ab3b-4b9b-9e16-7a1891e8cb2f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 2d416432aad9d5654aefd8c63b84b6ae18967515
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-web-deployment-using-visual-studio-troubleshooting"></a><span data-ttu-id="02c2a-103">使用 Visual Studio 的 ASP.NET Web 部署： 故障排除</span><span class="sxs-lookup"><span data-stu-id="02c2a-103">ASP.NET Web Deployment using Visual Studio: Troubleshooting</span></span>
====================
<span data-ttu-id="02c2a-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="02c2a-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="02c2a-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="02c2a-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="02c2a-106">本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，通过使用 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="02c2a-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="02c2a-107">有关序列的信息，请参阅[序列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="02c2a-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


<span data-ttu-id="02c2a-108">本页介绍通过使用 Visual Studio 部署 ASP.NET web 应用程序时可能出现的一些常见问题。</span><span class="sxs-lookup"><span data-stu-id="02c2a-108">This page describes some common problems that may arise when you deploy an ASP.NET web application by using Visual Studio.</span></span> <span data-ttu-id="02c2a-109">每个提供了一个或多个可能的原因和相应的解决方案。</span><span class="sxs-lookup"><span data-stu-id="02c2a-109">For each one, one or more possible causes and corresponding solutions are provided.</span></span>

<span data-ttu-id="02c2a-110">所示的方案适用于 Azure 和第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="02c2a-110">The scenarios shown apply to both Azure and third-party hosting providers.</span></span> <span data-ttu-id="02c2a-111">有关解决在 Azure App Service 中的 web 应用的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="02c2a-111">For more information about troubleshooting web apps in Azure App Service, see the following resources:</span></span>

- [<span data-ttu-id="02c2a-112">对 Azure App Service 中使用 Visual Studio 中的 web 应用进行故障排除</span><span class="sxs-lookup"><span data-stu-id="02c2a-112">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)
- [<span data-ttu-id="02c2a-113">在 Azure App Service 中监视 Web Apps</span><span class="sxs-lookup"><span data-stu-id="02c2a-113">Monitor Web Apps in Azure App Service</span></span>](https://azure.microsoft.com/en-us/documentation/articles/web-sites-monitor//)
- <span data-ttu-id="02c2a-114">[宣布的 Windows Azure SDK 2.0 for.NET 的发布](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net)（ScottGu 的博客，演示如何获取 Visual Studio 中的诊断日志）</span><span class="sxs-lookup"><span data-stu-id="02c2a-114">[Announcing the release of Windows Azure SDK 2.0 for .NET](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net) (ScottGu's blog, shows how to get diagnostic logs in Visual Studio)</span></span>

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a><span data-ttu-id="02c2a-115">服务器错误 '/' 应用程序-中当前的自定义错误设置防止错误的详细信息其他人远程查看</span><span class="sxs-lookup"><span data-stu-id="02c2a-115">Server Error in '/' Application - Current Custom Error Settings Prevent Details of the Error from Being Viewed Remotely</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-116">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-116">Scenario</span></span>

<span data-ttu-id="02c2a-117">部署到远程主机的站点之后, 你将收到错误消息，提及的 Web.config 文件中的 customErrors 设置，但并不指示错误的实际原因是：</span><span class="sxs-lookup"><span data-stu-id="02c2a-117">After deploying a site to a remote host, you get an error message that mentions the customErrors setting in the Web.config file but doesn't indicate what the actual cause of the error was:</span></span>

[!code-xml[Main](troubleshooting/samples/sample1.xml)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-118">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-118">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-119">默认情况下，ASP.NET 仅在本地计算机上运行 web 应用程序时显示详细的错误信息。</span><span class="sxs-lookup"><span data-stu-id="02c2a-119">By default, ASP.NET shows detailed error information only when your web application is running on the local computer.</span></span> <span data-ttu-id="02c2a-120">通常你不想要在 web 应用程序是在 Internet 上公开提供的因为黑客可能能够使用此信息来查找应用程序中的漏洞时显示详细的错误信息。</span><span class="sxs-lookup"><span data-stu-id="02c2a-120">Generally you don't want to display detailed error information when your web application is publicly available over the Internet, because hackers may be able to use this information to find vulnerabilities in the application.</span></span> <span data-ttu-id="02c2a-121">但是，当要部署的站点或更新到站点，有时内容将会出错，您需要先获取实际错误消息。</span><span class="sxs-lookup"><span data-stu-id="02c2a-121">However, when you are deploying a site or updates to a site, sometimes something will go wrong and you need to get the actual error message.</span></span>

<span data-ttu-id="02c2a-122">若要启用要在远程主机上运行时显示详细的错误消息的应用程序，请编辑要设置 customErrors 模式、 重新部署应用程序，并再次运行应用程序的 Web.config 文件：</span><span class="sxs-lookup"><span data-stu-id="02c2a-122">To enable the application to display detailed error messages when it runs on the remote host, edit the Web.config file to set customErrors mode off, redeploy the application, and run the application again:</span></span>

1. <span data-ttu-id="02c2a-123">如果应用程序 Web.config 文件中 thesystem.web 元素具有 acustomErrors 元素，themode 将属性更改为"关闭"。</span><span class="sxs-lookup"><span data-stu-id="02c2a-123">If the application Web.config file has acustomErrors element in thesystem.web element, change themode attribute to "off".</span></span> <span data-ttu-id="02c2a-124">否则 acustomErrors 元素 thesystem.web 在元素中添加 themode 特性设置为"off"，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="02c2a-124">Otherwise add acustomErrors element in thesystem.web element with themode attribute set to "off", as shown in the following example:</span></span> 

    [!code-xml[Main](troubleshooting/samples/sample2.xml)]
2. <span data-ttu-id="02c2a-125">部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="02c2a-125">Deploy the application.</span></span>
3. <span data-ttu-id="02c2a-126">运行应用程序并重复执行任何你此前导致发生错误。</span><span class="sxs-lookup"><span data-stu-id="02c2a-126">Run the application and repeat whatever you did earlier that caused the error to occur.</span></span> <span data-ttu-id="02c2a-127">现在，你可以看到什么是实际错误消息。</span><span class="sxs-lookup"><span data-stu-id="02c2a-127">Now you can see what the actual error message is.</span></span>
4. <span data-ttu-id="02c2a-128">在纠正错误，还原原始的 customErrors 设置并重新部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="02c2a-128">When you have resolved the error, restore the original customErrors setting and redeploy the application.</span></span>

## <a name="cannot-createshadow-copy-contosouniversity-when-that-file-already-exists"></a><span data-ttu-id="02c2a-129">无法创建/卷影副本 ContosoUniversity 该文件已存在时。</span><span class="sxs-lookup"><span data-stu-id="02c2a-129">Cannot create/shadow copy 'ContosoUniversity' when that file already exists.</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-130">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-130">Scenario</span></span>

<span data-ttu-id="02c2a-131">当你尝试运行 Visual Studio 中的项目会得到一个类似下面的示例消息的错误页：</span><span class="sxs-lookup"><span data-stu-id="02c2a-131">When you try to run a project in Visual Studio you get an error page with a message like the following example:</span></span>

<span data-ttu-id="02c2a-132">'/' 应用程序中的服务器错误。</span><span class="sxs-lookup"><span data-stu-id="02c2a-132">Server Error in '/' Application.</span></span> <span data-ttu-id="02c2a-133">无法创建/卷影副本 ContosoUniversity 该文件已存在时。</span><span class="sxs-lookup"><span data-stu-id="02c2a-133">Cannot create/shadow copy 'ContosoUniversity' when that file already exists.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-134">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-134">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-135">稍等片刻并刷新浏览器中，或重新编译该站点，以及尝试再次运行。</span><span class="sxs-lookup"><span data-stu-id="02c2a-135">Wait a minute and refresh the browser, or recompile the site and try running it again.</span></span>

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a><span data-ttu-id="02c2a-136">访问被拒绝网页中使用 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="02c2a-136">Access is Denied in a Web Page that Uses SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-137">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-137">Scenario</span></span>

<span data-ttu-id="02c2a-138">在部署使用 SQL Server Compact 的站点访问数据库的已部署站点中运行某个页面时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="02c2a-138">When you deploy a site that uses SQL Server Compact and you run a page in the deployed site that accesses the database, you see the following error message:</span></span>

<span data-ttu-id="02c2a-139">拒绝访问。</span><span class="sxs-lookup"><span data-stu-id="02c2a-139">Access is denied.</span></span> <span data-ttu-id="02c2a-140">(异常来自 HRESULT: 0x80070005 (E\_ACCESSDENIED))</span><span class="sxs-lookup"><span data-stu-id="02c2a-140">(Exception from HRESULT: 0x80070005 (E\_ACCESSDENIED))</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-141">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-141">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-142">服务器上的网络服务帐户需要能够读取 SQL 服务 Compact 中的本机二进制文件*bin\amd64*或*bin\x86*文件夹中，但它没有读取这些文件夹的权限。</span><span class="sxs-lookup"><span data-stu-id="02c2a-142">The NETWORK SERVICE account on the server needs to be able to read SQL Service Compact native binaries that are in the *bin\amd64* or *bin\x86* folder, but it does not have read permissions for those folders.</span></span> <span data-ttu-id="02c2a-143">设置在读取网络服务的权限*bin*文件夹，同时确保扩展的子文件夹的权限。</span><span class="sxs-lookup"><span data-stu-id="02c2a-143">Set read permission for NETWORK SERVICE on the *bin* folder, making sure to extend the permissions to subfolders.</span></span>

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a><span data-ttu-id="02c2a-144">无法读取配置文件由于权限不足而</span><span class="sxs-lookup"><span data-stu-id="02c2a-144">Cannot Read Configuration File Due to Insufficient Permissions</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-145">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-145">Scenario</span></span>

<span data-ttu-id="02c2a-146">当你单击 Visual Studio 发布按钮以应用程序部署到 IIS 在本地计算机，发布失败和**输出**窗口将显示一条错误消息类似于此：</span><span class="sxs-lookup"><span data-stu-id="02c2a-146">When you click the Visual Studio publish button to deploy an application to IIS on your local machine, publishing fails and the **Output** window shows an error message similar to this:</span></span>

<span data-ttu-id="02c2a-147">读取 IIS 配置文件机/重定向时出错。</span><span class="sxs-lookup"><span data-stu-id="02c2a-147">An error occurred when reading the IIS Configuration File 'MACHINE/REDIRECTION'.</span></span> <span data-ttu-id="02c2a-148">执行此操作的标识已...错误： 无法读取配置文件，因为没有足够的权限。</span><span class="sxs-lookup"><span data-stu-id="02c2a-148">The identity performing this operation was ... Error: Cannot read configuration file due to insufficient permissions.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-149">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-149">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-150">若要使用一次单击将发布到 IIS 在本地计算机上，你必须具有管理员权限运行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="02c2a-150">To use one-click publish to IIS on your local machine, you must be running Visual Studio with administrator permissions.</span></span> <span data-ttu-id="02c2a-151">关闭 Visual Studio 并重新启动它具有管理员权限。</span><span class="sxs-lookup"><span data-stu-id="02c2a-151">Close Visual Studio and restart it with administrator permissions.</span></span>

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a><span data-ttu-id="02c2a-152">无法连接到目标计算机...使用指定的进程</span><span class="sxs-lookup"><span data-stu-id="02c2a-152">Could Not Connect to the Destination Computer ... Using the Specified Process</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-153">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-153">Scenario</span></span>

<span data-ttu-id="02c2a-154">当你单击 Visual Studio 发布按钮以部署应用程序，发布失败和**输出**窗口将显示一条错误消息类似于此：</span><span class="sxs-lookup"><span data-stu-id="02c2a-154">When you click the Visual Studio publish button to deploy an application, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](troubleshooting/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-155">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-155">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-156">代理服务器中断与目标服务器的通信。</span><span class="sxs-lookup"><span data-stu-id="02c2a-156">A proxy server is interrupting communication with the destination server.</span></span> <span data-ttu-id="02c2a-157">从 Windows 控制面板或 Internet Explorer 中，选择**Internet 选项**和选择**连接**选项卡。在**互联**对话框中，单击**LAN 设置**。</span><span class="sxs-lookup"><span data-stu-id="02c2a-157">From the Windows Control Panel or in Internet Explorer, select **Internet Options** and select the **Connections** tab. In the **Internet Properties** dialog box, click **LAN Settings**.</span></span> <span data-ttu-id="02c2a-158">在**局域网 (LAN) 设置**对话框中，清除**自动检测设置**复选框。</span><span class="sxs-lookup"><span data-stu-id="02c2a-158">In the **Local Area Network (LAN) Settings** dialog box, clear the **Automatically detect settings** checkbox.</span></span> <span data-ttu-id="02c2a-159">然后再次单击发布按钮。</span><span class="sxs-lookup"><span data-stu-id="02c2a-159">Then click the publish button again.</span></span>

<span data-ttu-id="02c2a-160">如果问题仍然存在，请与系统管理员联系，以确定什么可通过代理或防火墙设置。</span><span class="sxs-lookup"><span data-stu-id="02c2a-160">If the problem persists, contact your system administrator to determine what can be done with proxy or firewall settings.</span></span> <span data-ttu-id="02c2a-161">因为 Web 部署为 Web 管理服务部署 (8172); 使用非标准端口仍然出现该问题对于其他连接，Web 部署使用端口 80。</span><span class="sxs-lookup"><span data-stu-id="02c2a-161">The problem happens because Web Deploy uses a non-standard port for Web Management Service deployment (8172); for other connections, Web Deploy uses port 80.</span></span> <span data-ttu-id="02c2a-162">当将部署到第三方托管提供商时，你通常使用 Web 管理服务。</span><span class="sxs-lookup"><span data-stu-id="02c2a-162">When you are deploying to a third-party hosting provider, you are typically using the Web Management Service.</span></span>

## <a name="default-net-40-application-pool-does-not-exist"></a><span data-ttu-id="02c2a-163">默认.NET 4.0 的应用程序池不存在</span><span class="sxs-lookup"><span data-stu-id="02c2a-163">Default .NET 4.0 Application Pool Does Not Exist</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-164">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-164">Scenario</span></span>

<span data-ttu-id="02c2a-165">当你部署的应用程序需要.NET Framework 4 时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="02c2a-165">When you deploy an application that requires the .NET Framework 4, you see the following error message:</span></span>

<span data-ttu-id="02c2a-166">默认.NET 4.0 应用程序池不存在或无法添加应用程序。</span><span class="sxs-lookup"><span data-stu-id="02c2a-166">The default .NET 4.0 application pool does not exist or the application could not be added.</span></span> <span data-ttu-id="02c2a-167">请验证此计算机上安装 ASP.NET 4.0。</span><span class="sxs-lookup"><span data-stu-id="02c2a-167">Please verify that ASP.NET 4.0 is installed on this machine.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-168">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-168">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-169">ASP.NET 4 未安装在 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="02c2a-169">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="02c2a-170">如果您要部署到的服务器是开发计算机，并且在其上安装 Visual Studio 2010，ASP.NET 4 的计算机上安装，但可能未安装在 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="02c2a-170">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="02c2a-171">在服务器上要部署到，打开提升的命令提示符并安装在 IIS 中的 ASP.NET 4 中，通过运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="02c2a-171">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample4.cmd)]

<span data-ttu-id="02c2a-172">你可能还需要手动设置默认应用程序池的.NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="02c2a-172">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="02c2a-173">有关详细信息，请参阅本系列中的测试环境教程作为的部署到 IIS。</span><span class="sxs-lookup"><span data-stu-id="02c2a-173">For more information, see the Deploying to IIS as a Test Environment tutorial in this series.</span></span>

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a><span data-ttu-id="02c2a-174">初始化字符串的格式不符合从索引 0 处开始的规范。</span><span class="sxs-lookup"><span data-stu-id="02c2a-174">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-175">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-175">Scenario</span></span>

<span data-ttu-id="02c2a-176">部署应用程序使用一次单击后发布，当你运行的页访问数据库获得以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="02c2a-176">After you deploy an application using one-click publish, when you run a page that accesses the database you get the following error message:</span></span>

<span data-ttu-id="02c2a-177">初始化字符串的格式不符合从索引 0 处开始的规范。</span><span class="sxs-lookup"><span data-stu-id="02c2a-177">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-178">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-178">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-179">打开*Web.config*中已部署的站点并查看连接字符串值是否以 $ 开头的文件 (ReplacableToken\_，下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="02c2a-179">Open the *Web.config* file in the deployed site and check to see whether the connection string values begin with $(ReplacableToken\_, as in the following example:</span></span>

[!code-xml[Main](troubleshooting/samples/sample5.xml)]

<span data-ttu-id="02c2a-180">如果连接字符串看上去像此示例中，编辑项目文件并将以下属性添加到为所有生成配置 PropertyGroup 元素：</span><span class="sxs-lookup"><span data-stu-id="02c2a-180">If the connection strings look like this example, edit the project file and add the following property to the PropertyGroup element that is for all build configurations:</span></span>

[!code-xml[Main](troubleshooting/samples/sample6.xml)]

<span data-ttu-id="02c2a-181">然后重新部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="02c2a-181">Then redeploy the application.</span></span>

## <a name="http-500-internal-server-error"></a><span data-ttu-id="02c2a-182">HTTP 500 内部服务器错误</span><span class="sxs-lookup"><span data-stu-id="02c2a-182">HTTP 500 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-183">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-183">Scenario</span></span>

<span data-ttu-id="02c2a-184">运行已部署的站点时，你将看到以下错误消息，没有特定信息，该值指示错误的原因：</span><span class="sxs-lookup"><span data-stu-id="02c2a-184">When you run the deployed site, you see the following error message without specific information indicating the cause of the error:</span></span>

<span data-ttu-id="02c2a-185">HTTP 错误 500-内部服务器错误。</span><span class="sxs-lookup"><span data-stu-id="02c2a-185">HTTP Error 500 - Internal Server Error.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-186">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-186">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-187">有许多原因的 500 错误，但如果按照这些教程的一个可能原因是可将一个 XML 元素放入其中一个 Web.config 转换文件中错误的位置。</span><span class="sxs-lookup"><span data-stu-id="02c2a-187">There are many causes of 500 errors, but one possible cause if you are following these tutorials is that you put an XML element in the wrong place in one of the Web.config transformation files.</span></span> <span data-ttu-id="02c2a-188">例如，你会遇到此错误，如果你将插入的转换&lt;位置&gt;元素下的&lt;system.web&gt;而不是直接在&lt;配置&gt;。</span><span class="sxs-lookup"><span data-stu-id="02c2a-188">For example, you would get this error if you put the transformation that inserts a &lt;location&gt; element under &lt;system.web&gt; instead of directly under &lt;configuration&gt;.</span></span> <span data-ttu-id="02c2a-189">Web.config 转换预览功能可用于验证转换按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="02c2a-189">You can use the Web.config transform preview feature to verify that transformations are working as intended.</span></span> <span data-ttu-id="02c2a-190">如果你找到编码不正确的转换的解决方案是更正转换文件并重新部署。</span><span class="sxs-lookup"><span data-stu-id="02c2a-190">The solution if you find a transform that was coded incorrectly is to correct the transformation file and redeploy.</span></span> <span data-ttu-id="02c2a-191">如果错误并不明确的请尝试注释掉转换，然后重新部署以查看哪一个导致 500 错误。</span><span class="sxs-lookup"><span data-stu-id="02c2a-191">If an error isn't obvious, try commenting out transforms and redeploying to see which one is causing the 500 error.</span></span>

## <a name="http-50021-internal-server-error"></a><span data-ttu-id="02c2a-192">HTTP 500.21 内部服务器错误</span><span class="sxs-lookup"><span data-stu-id="02c2a-192">HTTP 500.21 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-193">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-193">Scenario</span></span>

<span data-ttu-id="02c2a-194">运行已部署的站点时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="02c2a-194">When you run the deployed site, you see the following error message:</span></span>

<span data-ttu-id="02c2a-195">HTTP 错误 500.21-内部服务器错误。</span><span class="sxs-lookup"><span data-stu-id="02c2a-195">HTTP Error 500.21 - Internal Server Error.</span></span> <span data-ttu-id="02c2a-196">"PageHandlerFactory 集成"的处理程序有一个错误模块"ManagedPipelineHandler"在其模块列表。</span><span class="sxs-lookup"><span data-stu-id="02c2a-196">Handler "PageHandlerFactory-Integrated" has a bad module "ManagedPipelineHandler" in its module list.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-197">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-197">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-198">你已为其部署 ASP.NET 4 中，但 ASP.NET 4 未注册在 IIS 中在服务器的目标站点。</span><span class="sxs-lookup"><span data-stu-id="02c2a-198">The site you have deployed targets ASP.NET 4, but ASP.NET 4 is not registered in IIS on the server.</span></span> <span data-ttu-id="02c2a-199">在服务器上打开提升的命令提示符，并通过运行以下命令来注册 ASP.NET 4:</span><span class="sxs-lookup"><span data-stu-id="02c2a-199">On the server open an elevated command prompt and register ASP.NET 4 by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample7.cmd)]

<span data-ttu-id="02c2a-200">你可能还需要手动设置默认应用程序池的.NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="02c2a-200">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="02c2a-201">有关详细信息，请参阅本系列中的测试环境教程作为的部署到 IIS。</span><span class="sxs-lookup"><span data-stu-id="02c2a-201">For more information, see the Deploying to IIS as a Test Environment tutorial in this series.</span></span>

## <a name="login-failed-opening-sql-server-express-database-in-appdata"></a><span data-ttu-id="02c2a-202">登录失败打开 SQL Server Express 数据库中应用\_数据</span><span class="sxs-lookup"><span data-stu-id="02c2a-202">Login Failed Opening SQL Server Express Database in App\_Data</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-203">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-203">Scenario</span></span>

<span data-ttu-id="02c2a-204">您提供更新*Web.config*文件连接字符串以指向 SQL Server Express 数据库作为*.mdf*文件在你*应用\_数据*文件夹中和第一个运行应用程序，你看到以下错误消息的时间：</span><span class="sxs-lookup"><span data-stu-id="02c2a-204">You updated the *Web.config* file connection string to point to a SQL Server Express database as an *.mdf* file in your *App\_Data* folder, and the first time you run the application you see the following error message:</span></span>

<span data-ttu-id="02c2a-205">System.Data.SqlClient.SqlException： 无法打开数据库"DatabaseName"该登录请求的。</span><span class="sxs-lookup"><span data-stu-id="02c2a-205">System.Data.SqlClient.SqlException: Cannot open database "DatabaseName" requested by the login.</span></span> <span data-ttu-id="02c2a-206">登录失败。</span><span class="sxs-lookup"><span data-stu-id="02c2a-206">The login failed.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-207">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-207">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-208">名称*.mdf*文件不能匹配任何已曾经存在你计算机的 SQL Server Express 数据库的名称，即使你删除*.mdf*先前存在的数据库文件。</span><span class="sxs-lookup"><span data-stu-id="02c2a-208">The name of the *.mdf* file cannot match the name of any SQL Server Express database that has ever existed on your computer, even if you deleted the *.mdf* file of the previously existing database.</span></span> <span data-ttu-id="02c2a-209">更改的名称*.mdf*从未为数据库名称和更改使用的名称的文件*Web.config*文件以使用新名称。</span><span class="sxs-lookup"><span data-stu-id="02c2a-209">Change the name of the *.mdf* file to a name that has never been used as a database name and change the *Web.config* file to use the new name.</span></span> <span data-ttu-id="02c2a-210">作为替代方法，你可以使用[SQL Server Management Studio Express](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=7593)删除先前存在的 SQL Server Express 数据库。</span><span class="sxs-lookup"><span data-stu-id="02c2a-210">As an alternative, you can use [SQL Server Management Studio Express](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=7593) to delete previously existing SQL Server Express databases.</span></span>

## <a name="model-compatibility-cannot-be-checked"></a><span data-ttu-id="02c2a-211">模型兼容性无法检查</span><span class="sxs-lookup"><span data-stu-id="02c2a-211">Model Compatibility Cannot be Checked</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-212">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-212">Scenario</span></span>

<span data-ttu-id="02c2a-213">您提供更新*Web.config*文件连接字符串以指向新的 SQL Server Express 数据库，并运行应用程序首次你看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="02c2a-213">You updated the *Web.config* file connection string to point to a new SQL Server Express database, and the first time you run the application you see the following error message:</span></span>

<span data-ttu-id="02c2a-214">无法检查模型兼容，因为数据库不包含模型元数据。</span><span class="sxs-lookup"><span data-stu-id="02c2a-214">Model compatibility cannot be checked because the database does not contain model metadata.</span></span> <span data-ttu-id="02c2a-215">确保 IncludeMetadataConvention 验证已添加到 DbModelBuilder 约定。</span><span class="sxs-lookup"><span data-stu-id="02c2a-215">Ensure that IncludeMetadataConvention has been added to the DbModelBuilder conventions.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-216">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-216">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-217">如果你在计算机上，数据库可能已存在与某些表之前，已曾经使用 Web.config 文件中放置的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="02c2a-217">If the database name you put in the Web.config file was ever used before on your computer, a database might already exist with some tables in it.</span></span> <span data-ttu-id="02c2a-218">选择尚未使用在之前的计算机和更改的新名称*Web.config*文件以点以使用此新的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="02c2a-218">Select a new name that has not been used on your computer before and change the *Web.config* file to point to use this new database name.</span></span> <span data-ttu-id="02c2a-219">作为替代方法，你可以使用[SQL Server Express 实用工具](https://www.microsoft.com/en-us/download/details.aspx?DisplayLang=en&amp;id=3990)或[SQL Server Management Studio Express](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=7593)删除现有数据库。</span><span class="sxs-lookup"><span data-stu-id="02c2a-219">As an alternative, you can use [SQL Server Express Utility](https://www.microsoft.com/en-us/download/details.aspx?DisplayLang=en&amp;id=3990) or [SQL Server Management Studio Express](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=7593) to delete the existing database.</span></span>

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a><span data-ttu-id="02c2a-220">SQL 错误时的脚本尝试创建用户或角色</span><span class="sxs-lookup"><span data-stu-id="02c2a-220">SQL Error When a Script Attempts to Create Users or Roles</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-221">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-221">Scenario</span></span>

<span data-ttu-id="02c2a-222">您要使用在上配置的数据库部署**打包/发布 SQL**选项卡上，在部署过程中运行的 SQL 脚本包括 Create User 或创建角色命令和脚本执行失败时执行这些命令。</span><span class="sxs-lookup"><span data-stu-id="02c2a-222">You are using database deployment configured on the **Package/Publish SQL** tab, SQL scripts that run during deployment include Create User or Create Role commands, and script execution fails when those commands are executed.</span></span> <span data-ttu-id="02c2a-223">你可能会看到更多详细消息，如下所示：</span><span class="sxs-lookup"><span data-stu-id="02c2a-223">You might see more detailed messages, such as the following:</span></span>

[!code-console[Main](troubleshooting/samples/sample8.cmd)]

<span data-ttu-id="02c2a-224">如果你已配置中的数据库部署时会发生此错误**发布 Web**向导而不是**打包/发布 SQL**选项卡上，创建中的线程[配置和部署](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)论坛和解决方案将添加到此故障排除的页面。</span><span class="sxs-lookup"><span data-stu-id="02c2a-224">If this error occurs when you have configured database deployment in the **Publish Web** wizard rather than the **Package/Publish SQL** tab, create a thread in the [Configuration and Deployment](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) forum, and the solution will be added to this troubleshooting page.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-225">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-225">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-226">用来执行部署的用户帐户没有权限来创建用户或角色。</span><span class="sxs-lookup"><span data-stu-id="02c2a-226">The user account you are using to perform deployment does not have permission to create users or roles.</span></span> <span data-ttu-id="02c2a-227">例如，托管公司可能将分配数据库\_datareader，db\_datawriter，和 db\_ddladmin 角色到它为你设置的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="02c2a-227">For example, the hosting company might assign the db\_datareader, db\_datawriter, and db\_ddladmin roles to the user account that it sets up for you.</span></span> <span data-ttu-id="02c2a-228">这些是足够有关创建大多数的数据库对象，而不是创建用户或角色。</span><span class="sxs-lookup"><span data-stu-id="02c2a-228">These are sufficient for creating most database objects, but not for creating users or roles.</span></span> <span data-ttu-id="02c2a-229">若要避免错误的一种方法是通过从数据库部署中排除用户和角色。</span><span class="sxs-lookup"><span data-stu-id="02c2a-229">One way to avoid the error is by excluding users and roles from database deployment.</span></span> <span data-ttu-id="02c2a-230">可以通过编辑数据库的自动生成的脚本的 PreSource 元素，以使其包括以下属性来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="02c2a-230">You can do this by editing the PreSource element for the database's automatically generated script so that it includes the following attributes:</span></span>

[!code-console[Main](troubleshooting/samples/sample9.cmd)]

<span data-ttu-id="02c2a-231">有关如何编辑项目文件中的 PreSource 元素的信息，请参阅[如何： 编辑项目文件中的部署设置](https://msdn.microsoft.com/en-us/library/ff398069(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="02c2a-231">For information about how to edit the PreSource element in the project file, see [How to: Edit Deployment Settings in the Project File](https://msdn.microsoft.com/en-us/library/ff398069(v=vs.100).aspx).</span></span> <span data-ttu-id="02c2a-232">如果用户或开发数据库中的角色需要将位于目标数据库中，请与你托管提供商联系以获取帮助。</span><span class="sxs-lookup"><span data-stu-id="02c2a-232">If the users or roles in your development database need to be in the destination database, contact your hosting provider for assistance.</span></span>

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a><span data-ttu-id="02c2a-233">SQL Server 超时错误时在部署过程中运行自定义脚本</span><span class="sxs-lookup"><span data-stu-id="02c2a-233">SQL Server Timeout Error When Running Custom Scripts During Deployment</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-234">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-234">Scenario</span></span>

<span data-ttu-id="02c2a-235">您指定了自定义 SQL 脚本以在部署期间，运行，并且当 Web 部署运行它们时，它们的超时时间。</span><span class="sxs-lookup"><span data-stu-id="02c2a-235">You have specified custom SQL scripts to run during deployment, and when Web Deploy runs them, they time out.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-236">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-236">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-237">运行具有不同的事务模式的多个脚本可能导致超时错误。</span><span class="sxs-lookup"><span data-stu-id="02c2a-237">Running multiple scripts that have different transaction modes can cause time-out errors.</span></span> <span data-ttu-id="02c2a-238">默认情况下自动生成的脚本运行在事务中，但自定义脚本不这样做。</span><span class="sxs-lookup"><span data-stu-id="02c2a-238">By default, automatically generated scripts run in a transaction, but custom scripts do not.</span></span> <span data-ttu-id="02c2a-239">如果你选择**抽取数据和/或从现有数据库的架构**选项**打包/发布 SQL**选项卡上，如果你添加自定义 SQL 脚本，必须更改某些脚本上的事务设置，以便所有脚本都使用相同的事务设置。</span><span class="sxs-lookup"><span data-stu-id="02c2a-239">If you select the **Pull data and/or schema from an existing database** option on the **Package/Publish SQL** tab, and if you add a custom SQL script, you must change transaction settings on some scripts so that all scripts use the same transaction settings.</span></span> <span data-ttu-id="02c2a-240">有关详细信息，请参阅[如何： 部署数据库与 Web 应用程序项目](https://msdn.microsoft.com/en-us/library/dd465343.aspx)。</span><span class="sxs-lookup"><span data-stu-id="02c2a-240">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/en-us/library/dd465343.aspx).</span></span>

<span data-ttu-id="02c2a-241">如果你已配置事务设置，以便所有都相同，但仍遇到此错误，可能的解决方法是单独运行这些脚本。</span><span class="sxs-lookup"><span data-stu-id="02c2a-241">If you have configured transaction settings so that all are the same but still get this error, a possible workaround is to run the scripts separately.</span></span> <span data-ttu-id="02c2a-242">在**数据库脚本**网格中的**打包/发布**SQL 选项卡上，将其清除**包括**会导致超时错误，该脚本的复选框然后发布项目。</span><span class="sxs-lookup"><span data-stu-id="02c2a-242">In the **Database Scripts** grid in the **Package/Publish** SQL tab, clear the **Include** check box for the script that causes the timeout error, then publish the project.</span></span> <span data-ttu-id="02c2a-243">然后转回**数据库脚本**网格中，选择该脚本**包括**复选框，然后清除**包括**其他脚本对应的复选框。</span><span class="sxs-lookup"><span data-stu-id="02c2a-243">Then go back into the **Database Scripts** grid, select that script's **Include** check box, and clear the **Include** check boxes for the other scripts.</span></span> <span data-ttu-id="02c2a-244">然后再次发布该项目。</span><span class="sxs-lookup"><span data-stu-id="02c2a-244">Then publish the project again.</span></span> <span data-ttu-id="02c2a-245">发布时，此次运行时仅选择自定义的脚本。</span><span class="sxs-lookup"><span data-stu-id="02c2a-245">This time when you publish, only the selected custom script runs.</span></span>

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a><span data-ttu-id="02c2a-246">站点清单的流数据尚不可用</span><span class="sxs-lookup"><span data-stu-id="02c2a-246">Stream Data of Site Manifest Is Not Yet Available</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-247">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-247">Scenario</span></span>

<span data-ttu-id="02c2a-248">当你要安装包使用*deploy.cmd*文件使用 t （测试） 选项，请参阅以下的错误消息：</span><span class="sxs-lookup"><span data-stu-id="02c2a-248">When you are installing a package using the *deploy.cmd* file with the t (test) option, you see the following error message:</span></span>

<span data-ttu-id="02c2a-249">错误： 流数据的 sitemanifest/dbFullSql [@path= C:\TEMP\AdventureWorksGrant.sql']/sqlScript 尚不可用。</span><span class="sxs-lookup"><span data-stu-id="02c2a-249">Error: The stream data of 'sitemanifest/dbFullSql[@path='C:\TEMP\AdventureWorksGrant.sql']/sqlScript' is not yet available.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-250">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-250">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-251">错误消息表示命令无法生成测试报告。</span><span class="sxs-lookup"><span data-stu-id="02c2a-251">The error message means that the command cannot produce a test report.</span></span> <span data-ttu-id="02c2a-252">但是，如果你使用的 y （实际安装） 选项，可以运行该命令。</span><span class="sxs-lookup"><span data-stu-id="02c2a-252">However, the command might run if you use the y (actual installation) option.</span></span> <span data-ttu-id="02c2a-253">此消息仅指示在测试模式下运行该命令的问题。</span><span class="sxs-lookup"><span data-stu-id="02c2a-253">The message indicates only that there is a problem with running the command in test mode.</span></span>

## <a name="this-application-requires-managedruntimeversion-v40"></a><span data-ttu-id="02c2a-254">此应用程序需要 ManagedRuntimeVersion v4.0</span><span class="sxs-lookup"><span data-stu-id="02c2a-254">This Application Requires ManagedRuntimeVersion v4.0</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-255">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-255">Scenario</span></span>

<span data-ttu-id="02c2a-256">当你尝试部署时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="02c2a-256">When you attempt to deploy, you see the following error message:</span></span>

<span data-ttu-id="02c2a-257">你正在使用的应用程序池具有 managedRuntimeVersion 属性设置为 v2.0。</span><span class="sxs-lookup"><span data-stu-id="02c2a-257">The application pool that you are trying to use has the 'managedRuntimeVersion' property set to 'v2.0'.</span></span> <span data-ttu-id="02c2a-258">此应用程序需要 v4.0。</span><span class="sxs-lookup"><span data-stu-id="02c2a-258">This application requires 'v4.0'.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-259">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-259">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-260">ASP.NET 4 未安装在 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="02c2a-260">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="02c2a-261">如果您要部署到的服务器是开发计算机，并且在其上安装 Visual Studio 2010，ASP.NET 4 的计算机上安装，但可能未安装在 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="02c2a-261">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="02c2a-262">在服务器上要部署到，打开提升的命令提示符并安装在 IIS 中的 ASP.NET 4 中，通过运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="02c2a-262">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample10.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a><span data-ttu-id="02c2a-263">无法将 Microsoft.Web.Deployment.DeploymentProviderOptions 强制转换</span><span class="sxs-lookup"><span data-stu-id="02c2a-263">Unable to cast Microsoft.Web.Deployment.DeploymentProviderOptions</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-264">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-264">Scenario</span></span>

<span data-ttu-id="02c2a-265">在部署包时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="02c2a-265">When you are deploying a package, you see the following error message:</span></span>

<span data-ttu-id="02c2a-266">无法将类型 Microsoft.Web.Deployment.DeploymentProviderOptions 到 Microsoft.Web.Deployment.DeploymentProviderOptions 的对象强制转换。</span><span class="sxs-lookup"><span data-stu-id="02c2a-266">Unable to cast object of type 'Microsoft.Web.Deployment.DeploymentProviderOptions' to 'Microsoft.Web.Deployment.DeploymentProviderOptions'.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-267">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-267">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-268">你尝试部署从 IIS 管理器中使用 Web 部署 1.1 UI 到已安装的 Web 部署 2.0 的服务器。</span><span class="sxs-lookup"><span data-stu-id="02c2a-268">You are trying to deploy from IIS Manager using the Web Deploy 1.1 UI to a server that has Web Deploy 2.0 installed.</span></span> <span data-ttu-id="02c2a-269">如果你使用 IIS 的远程管理工具来部署通过导入包中，检查**新提供的功能**建立连接时的对话框。</span><span class="sxs-lookup"><span data-stu-id="02c2a-269">If you are using the IIS Remote Administration Tool to deploy by importing a package, check the **New Features Available** dialog box when you establish the connection.</span></span> <span data-ttu-id="02c2a-270">（此对话框中可能才会显示一次当首次建立连接。</span><span class="sxs-lookup"><span data-stu-id="02c2a-270">(This dialog box might only be shown once when the connection is first established.</span></span> <span data-ttu-id="02c2a-271">若要清除连接并重新启动，关闭 IIS 管理器和它再次启动通过输入 inetmgr/重置在命令提示符下。）如果列出的功能之一是**Web 部署 UI**，并且它有一个版本号低于 8，您要部署到的服务器可能必须 1.1 和 2.0 版的 Web 部署安装。</span><span class="sxs-lookup"><span data-stu-id="02c2a-271">To clear the connection and start over, close IIS Manager and start it up again by entering inetmgr /reset at the command prompt.) If one of the features listed is **Web Deploy UI**, and it has a version number lower than 8, the server you are deploying to might have both 1.1 and 2.0 versions of Web Deploy installed.</span></span> <span data-ttu-id="02c2a-272">若要从具有 2.0 安装的客户端部署，服务器必须仅 Web Deploy 2.0 安装。</span><span class="sxs-lookup"><span data-stu-id="02c2a-272">To deploy from a client that has 2.0 installed, the server must have only Web Deploy 2.0 installed.</span></span> <span data-ttu-id="02c2a-273">你将需要联系托管提供商若要解决此问题。</span><span class="sxs-lookup"><span data-stu-id="02c2a-273">You will have to contact your hosting provider to resolve this problem.</span></span>

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a><span data-ttu-id="02c2a-274">无法加载 SQL Server Compact 的本机组件</span><span class="sxs-lookup"><span data-stu-id="02c2a-274">Unable to load the native components of SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-275">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-275">Scenario</span></span>

<span data-ttu-id="02c2a-276">运行已部署的站点时，你将看到以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="02c2a-276">When you run the deployed site, you see the following error message:</span></span>

<span data-ttu-id="02c2a-277">无法加载 SQL Server Compact 版本 8482 的 ADO.NET 提供程序所对应的本机组件。</span><span class="sxs-lookup"><span data-stu-id="02c2a-277">Unable to load the native components of SQL Server Compact corresponding to the ADO.NET provider of version 8482.</span></span> <span data-ttu-id="02c2a-278">安装 SQL Server Compact 的正确版本。</span><span class="sxs-lookup"><span data-stu-id="02c2a-278">Install the correct version of SQL Server Compact.</span></span> <span data-ttu-id="02c2a-279">请参阅 KB 文章 974247 有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="02c2a-279">Refer to KB article 974247 for more details.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-280">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-280">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-281">已部署的站点并没有*amd64*和*x86*使用本机的程序集，该应用程序下的子文件夹*bin*文件夹。</span><span class="sxs-lookup"><span data-stu-id="02c2a-281">The deployed site does not have *amd64* and *x86* subfolders with the native assemblies in them under the application's *bin* folder.</span></span> <span data-ttu-id="02c2a-282">在上 SQL Server Compact 安装的计算机，本机程序集位于*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*。</span><span class="sxs-lookup"><span data-stu-id="02c2a-282">On a computer that has SQL Server Compact installed, the native assemblies are located in *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*.</span></span> <span data-ttu-id="02c2a-283">到正确的文件夹中的 Visual Studio 项目中获取正确的文件的最佳方法是安装 NuGet SqlServerCompact 包。</span><span class="sxs-lookup"><span data-stu-id="02c2a-283">The best way to get the correct files into the correct folders in a Visual Studio project is to install the NuGet SqlServerCompact package.</span></span> <span data-ttu-id="02c2a-284">包安装添加后期生成脚本，以将复制到本机程序集*amd64*和*x86*。</span><span class="sxs-lookup"><span data-stu-id="02c2a-284">Package installation adds a post-build script to copy the native assemblies into *amd64* and *x86*.</span></span> <span data-ttu-id="02c2a-285">为了使这些部署，但是，必须手动将其包含在项目中。</span><span class="sxs-lookup"><span data-stu-id="02c2a-285">In order for these to be deployed, however, you have to manually include them in the project.</span></span> <span data-ttu-id="02c2a-286">有关详细信息，请参阅[部署 SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教程。</span><span class="sxs-lookup"><span data-stu-id="02c2a-286">For more information, see the [Deploying SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a><span data-ttu-id="02c2a-287">部署 Entity Framework Code First 的应用程序后，"路径不是有效的"错误</span><span class="sxs-lookup"><span data-stu-id="02c2a-287">"Path is not valid" error after deploying an Entity Framework Code First application</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-288">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-288">Scenario</span></span>

<span data-ttu-id="02c2a-289">部署应用程序，如 SQL Server Compact 后者将其数据库存储在应用程序中的文件使用 Entity Framework Code First 迁移和 DBMS\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="02c2a-289">You deploy an application that uses Entity Framework Code First Migrations and a DBMS such as SQL Server Compact which stores its database in a file in the App\_Data folder.</span></span> <span data-ttu-id="02c2a-290">必须配置为在第一个部署之后创建数据库的 Code First 迁移。</span><span class="sxs-lookup"><span data-stu-id="02c2a-290">You have Code First Migrations configured to create the database after your first deployment.</span></span> <span data-ttu-id="02c2a-291">当你运行应用程序可以一条错误消息如下例所示：</span><span class="sxs-lookup"><span data-stu-id="02c2a-291">When you run the application you get an error message like the following example:</span></span>

<span data-ttu-id="02c2a-292">路径不是有效的。</span><span class="sxs-lookup"><span data-stu-id="02c2a-292">The path is not valid.</span></span> <span data-ttu-id="02c2a-293">检查数据库的目录。</span><span class="sxs-lookup"><span data-stu-id="02c2a-293">Check the directory for the database.</span></span> <span data-ttu-id="02c2a-294">[路径 = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf]</span><span class="sxs-lookup"><span data-stu-id="02c2a-294">[Path = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf ]</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-295">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-295">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-296">代码首先尝试创建数据库，但应用\_数据文件夹不存在。</span><span class="sxs-lookup"><span data-stu-id="02c2a-296">Code First is attempting to create the database but the App\_Data folder does not exist.</span></span> <span data-ttu-id="02c2a-297">未有任何文件*应用\_数据*文件夹时部署，或者与您选择**排除应用\_数据**上**打包/发布 Web**项目属性窗口选项卡。</span><span class="sxs-lookup"><span data-stu-id="02c2a-297">Either you didn't have any files in the *App\_Data* folder when you deployed, or you selected **Exclude App\_Data** on the **Package/Publish Web** tab of the Project Properties window.</span></span> <span data-ttu-id="02c2a-298">如果要复制到服务器的文件夹中不有任何文件，在部署过程不会在服务器上创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="02c2a-298">The deployment process won't create a folder on the server if there are no files in the folder to be copied to the server.</span></span> <span data-ttu-id="02c2a-299">如果您已经有站点中设置的数据库，在部署过程将删除的文件和*应用\_数据*文件夹本身如果你选择**删除目标位置的其他文件**中发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="02c2a-299">If you already had the database set up in the site, the deployment process will delete the files and the *App\_Data* folder itself if you selected **Remove additional files at destination** in the publish profile.</span></span> <span data-ttu-id="02c2a-300">若要解决此问题，将占位符文件，如中的.txt 文件*应用\_数据*文件夹，请确保你没有**排除应用\_数据**选择，并重新部署。</span><span class="sxs-lookup"><span data-stu-id="02c2a-300">To solve the problem, put a placeholder file such as a .txt file in the *App\_Data* folder, make sure you do not have **Exclude App\_Data** selected, and redeploy.</span></span>

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a><span data-ttu-id="02c2a-301">"不能使用已分开其基础 RCW 的 COM 对象"。</span><span class="sxs-lookup"><span data-stu-id="02c2a-301">"COM object that has been separated from its underlying RCW cannot be used."</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-302">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-302">Scenario</span></span>

<span data-ttu-id="02c2a-303">你已成功使用一键式发布来部署你的应用程序，然后你启动遇到此错误：</span><span class="sxs-lookup"><span data-stu-id="02c2a-303">You have been successfully using one-click publish to deploy your application and then you start getting this error:</span></span>

<span data-ttu-id="02c2a-304">Web 部署任务失败。</span><span class="sxs-lookup"><span data-stu-id="02c2a-304">Web deployment task failed.</span></span> <span data-ttu-id="02c2a-305">（无法完成对远程代理 URL https://serverurl.com/msdeploy.axd?site=sitename 的请求）。</span><span class="sxs-lookup"><span data-stu-id="02c2a-305">(Could not complete the request to remote agent URL 'https://serverurl.com/msdeploy.axd?site=sitename'.)</span></span>  
 <span data-ttu-id="02c2a-306">无法完成对远程代理 URL https://url/msdeploy.axd?site=sitename 请求。</span><span class="sxs-lookup"><span data-stu-id="02c2a-306">Could not complete the request to remote agent URL 'https://url/msdeploy.axd?site=sitename'.</span></span>  
<span data-ttu-id="02c2a-307">该请求已中止： 该请求已取消。</span><span class="sxs-lookup"><span data-stu-id="02c2a-307">The request was aborted: The request was canceled.</span></span>  
<span data-ttu-id="02c2a-308">无法使用已分开其基础 RCW 的 COM 对象。</span><span class="sxs-lookup"><span data-stu-id="02c2a-308">COM object that has been separated from its underlying RCW cannot be used.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-309">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-309">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-310">关闭和重新启动 Visual Studio 通常是所有需要来解决此错误。</span><span class="sxs-lookup"><span data-stu-id="02c2a-310">Closing and restarting Visual Studio is usually all that is required to resolve this error.</span></span>

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a><span data-ttu-id="02c2a-311">部署失败由于用户凭据用于发布没有 setACL 颁发机构</span><span class="sxs-lookup"><span data-stu-id="02c2a-311">Deployment Fails Because User Credentials Used for Publishing Don't Have setACL Authority</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-312">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-312">Scenario</span></span>

<span data-ttu-id="02c2a-313">发布将失败并出错类型的值，该值指示你没有设置文件夹权限 （所使用的用户帐户没有 setACL 机构） 的授权。</span><span class="sxs-lookup"><span data-stu-id="02c2a-313">Publishing fails with an error that indicates you don't have authority to set folder permissions (the user account you are using doesn't have setACL authority).</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-314">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-314">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-315">默认情况下，Visual Studio 集对站点的根文件夹的读取权限和写应用程序权限\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="02c2a-315">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="02c2a-316">如果您知道站点文件夹上的默认权限是否正确，并且不需要设置，则禁用此行为通过添加 **&lt;IncludeSetACLProviderOn 目标&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 到发布配置文件 （以影响一个配置文件） 或 （要影响的所有配置文件） 的 wpp.targets 文件。</span><span class="sxs-lookup"><span data-stu-id="02c2a-316">If you know that the default permissions on site folders are correct and do not need to be set, you disable this behavior by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="02c2a-317">有关如何编辑这些文件的信息，请参阅[如何： 编辑配置文件 (.pubxml) 文件中的部署设置](https://msdn.microsoft.com/en-us/library/ff398069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="02c2a-317">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/en-us/library/ff398069.aspx).</span></span>

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a><span data-ttu-id="02c2a-318">当应用程序尝试写入到应用程序文件夹时，访问被拒绝错误</span><span class="sxs-lookup"><span data-stu-id="02c2a-318">Access Denied Errors when the Application Tries to Write to an Application Folder</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-319">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-319">Scenario</span></span>

<span data-ttu-id="02c2a-320">你的应用程序错误时它将尝试创建或编辑的文件中的一个应用程序文件夹中，因为它不具有该文件夹的写权限。</span><span class="sxs-lookup"><span data-stu-id="02c2a-320">Your application errors when it tries to create or edit a file in one of the application folders, because it does not have write authority for that folder.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-321">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-321">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-322">默认情况下，Visual Studio 集对站点的根文件夹的读取权限和写应用程序权限\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="02c2a-322">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="02c2a-323">如果你的应用程序需要的子文件夹的写访问权限，你可以将该文件夹的权限设置为中设置文件夹权限和部署到生产环境教程在本系列中所示。</span><span class="sxs-lookup"><span data-stu-id="02c2a-323">If your application needs write access to a sub-folder, you can set permissions for that folder as shown in the Setting Folder Permissions and Deploying to the Production Environment tutorials in this series.</span></span> <span data-ttu-id="02c2a-324">如果你的应用程序需要的站点的根文件夹的写访问权限，则必须防止它在根文件夹上设置只读访问权限，通过添加 **&lt;IncludeSetACLProviderOn 目标&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 到发布配置文件 （以影响一个配置文件） 或 （要影响的所有配置文件） 的 wpp.targets 文件。</span><span class="sxs-lookup"><span data-stu-id="02c2a-324">If your application needs write access to the root folder of the site, you have to prevent it from setting read-only access on the root folder by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="02c2a-325">有关如何编辑这些文件的信息，请参阅[如何： 编辑配置文件 (.pubxml) 文件中的部署设置](https://msdn.microsoft.com/en-us/library/ff398069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="02c2a-325">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/en-us/library/ff398069.aspx).</span></span>

<a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a><span data-ttu-id="02c2a-326">配置错误的 targetFramework 特性引用晚于安装的.NET Framework 版本的版本</span><span class="sxs-lookup"><span data-stu-id="02c2a-326">Configuration Error - targetFramework attribute references a version that is later than the installed version of the .NET Framework</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-327">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-327">Scenario</span></span>

<span data-ttu-id="02c2a-328">已成功发布的 web 项目是面向 ASP.NET 4.5，但在 （使用在 customErrors 模式设置为"关闭"状态在 Web.config 文件中） 运行应用程序时您收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="02c2a-328">You successfully published a web project that targets ASP.NET 4.5, but when you run the application (with the customErrors mode set to "off" in the Web.config file) you get the following error:</span></span>

<span data-ttu-id="02c2a-329">TargetFramework 属性中&lt;编译&gt;仅对目标版本 4.0 和更高版本的.NET Framework，则使用 Web.config 文件的元素 (例如，&lt;编译 targetFramework ="4.0"&gt;').</span><span class="sxs-lookup"><span data-stu-id="02c2a-329">The 'targetFramework' attribute in the &lt;compilation&gt; element of the Web.config file is used only to target version 4.0 and later of the .NET Framework (for example, '&lt;compilation targetFramework="4.0"&gt;').</span></span> <span data-ttu-id="02c2a-330">TargetFramework 属性当前引用晚于安装的.NET Framework 版本的版本。</span><span class="sxs-lookup"><span data-stu-id="02c2a-330">The 'targetFramework' attribute currently references a version that is later than the installed version of the .NET Framework.</span></span> <span data-ttu-id="02c2a-331">指定有效的目标版本的.NET Framework 中，或安装所需的.NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="02c2a-331">Specify a valid target version of the .NET Framework, or install the required version of the .NET Framework.</span></span>

<span data-ttu-id="02c2a-332">错误页的源错误框突出从 Web.config 的以下行显示为错误的原因：</span><span class="sxs-lookup"><span data-stu-id="02c2a-332">The Source Error box of the error page highlights the following line from Web.config as the cause of the error:</span></span>

<span data-ttu-id="02c2a-333">&lt;编译 targetFramework ="4.5"/&gt;</span><span class="sxs-lookup"><span data-stu-id="02c2a-333">&lt;compilation targetFramework="4.5" /&gt;</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-334">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-334">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-335">服务器不支持 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="02c2a-335">The server does not support ASP.NET 4.5.</span></span> <span data-ttu-id="02c2a-336">联系托管提供商来确定何时及是否可添加对 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="02c2a-336">Contact the hosting provider to determine when and if support for ASP.NET 4.5 can be added.</span></span> <span data-ttu-id="02c2a-337">如果升级服务器不是一个选项，则必须部署面向 4 或更早版本的 ASP.NET web 项目相反。</span><span class="sxs-lookup"><span data-stu-id="02c2a-337">If upgrading the server is not an option, you have to deploy a web project that targets ASP.NET 4 or earlier instead.</span></span>

<span data-ttu-id="02c2a-338">如果将 ASP.NET 4 或更早版本的 web 项目部署到相同的目标中，选择**删除目标位置的其他文件**上的复选框**设置**选项卡**发布 Web**向导。</span><span class="sxs-lookup"><span data-stu-id="02c2a-338">If you deploy an ASP.NET 4 or earlier web project to the same destination, select the **Remove additional files at destination** check box on the **Settings** tab of the **Publish Web** wizard.</span></span> <span data-ttu-id="02c2a-339">如果你未选中**删除目标位置的其他文件**，你将继续获取配置错误页。</span><span class="sxs-lookup"><span data-stu-id="02c2a-339">If you don't select **Remove additional files at destination**, you will continue to get the Configuration Error page.</span></span>

<span data-ttu-id="02c2a-340">项目**属性**windows 包含目标框架下拉列表，但你不能解决此问题通过只需更改，从**.NET Framework 4.5**到**.NET Framework 4**.</span><span class="sxs-lookup"><span data-stu-id="02c2a-340">The project **Properties** windows includes a Target framework drop-down list, but you can't resolve this problem by just changing that from **.NET Framework 4.5** to **.NET Framework 4**.</span></span> <span data-ttu-id="02c2a-341">如果你将目标框架更改为更早版本的 framework 版本时，项目将仍具有对的更高版本的 framework 版本的程序集的引用，而不会运行。</span><span class="sxs-lookup"><span data-stu-id="02c2a-341">If you change the target framework to an earlier framework version, the project will still have references to the later framework version's assemblies and will not run.</span></span> <span data-ttu-id="02c2a-342">你必须手动更改这些引用，或创建新的项目面向.NET Framework 4 或更早版本。</span><span class="sxs-lookup"><span data-stu-id="02c2a-342">You have to manually change those references or create a new project that targets .NET Framework 4 or earlier.</span></span> <span data-ttu-id="02c2a-343">有关详细信息，请参阅[.NET Framework 面向网站](https://msdn.microsoft.com/en-us/library/bb398791(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="02c2a-343">For more information, see [.NET Framework Targeting for Web Sites](https://msdn.microsoft.com/en-us/library/bb398791(v=vs.100).aspx).</span></span>

## <a name="medium-trust-errors"></a><span data-ttu-id="02c2a-344">中级信任错误</span><span class="sxs-lookup"><span data-stu-id="02c2a-344">Medium Trust Errors</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-345">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-345">Scenario</span></span>

<span data-ttu-id="02c2a-346">在生产环境中运行你的应用程序时，它将获取与中等信任相关的错误。</span><span class="sxs-lookup"><span data-stu-id="02c2a-346">When you run your application in production, it gets an error related to medium trust.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-347">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-347">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-348">许多第三方托管提供商在中等信任中，这意味着它不允许执行的操作的一些事项中运行您的网站。</span><span class="sxs-lookup"><span data-stu-id="02c2a-348">Many third-party hosting providers run your web site in medium trust, which means that there are some things it isn't allowed to do.</span></span> <span data-ttu-id="02c2a-349">例如，应用程序代码不能访问 Windows 注册表和无法读取或写入应用程序的文件夹层次结构之外的文件。</span><span class="sxs-lookup"><span data-stu-id="02c2a-349">For example, application code can't access the Windows registry and can't read or write files that are outside of your application's folder hierarchy.</span></span> <span data-ttu-id="02c2a-350">默认情况下你的应用程序运行*完全信任*在本地计算机，这意味着应用程序可能能够执行时将其部署到生产环境将失败的操作。</span><span class="sxs-lookup"><span data-stu-id="02c2a-350">By default your application runs in *full trust* on your local computer, which means that the application might be able to do things that would fail when you deploy it to production.</span></span>

<span data-ttu-id="02c2a-351">你可以配置要在中等信任中在本地 IIS 环境中运行以解决问题的应用程序。</span><span class="sxs-lookup"><span data-stu-id="02c2a-351">You can configure the application to run in medium trust in the local IIS environment in order to troubleshoot.</span></span> <span data-ttu-id="02c2a-352">为此，请打开应用程序*Web.config*文件，并添加**信任**中的元素**system.web**元素，如本示例中所示。</span><span class="sxs-lookup"><span data-stu-id="02c2a-352">To do that, open the application *Web.config* file, and add a **trust** element in the **system.web** element, as shown in this example.</span></span>

[!code-xml[Main](troubleshooting/samples/sample11.xml)]

<span data-ttu-id="02c2a-353">即使在本地计算机上，现在在 IIS 中的中级信任应用程序将运行。</span><span class="sxs-lookup"><span data-stu-id="02c2a-353">The application will now run in medium trust in IIS even on your local computer.</span></span>

<span data-ttu-id="02c2a-354">不要此如果部署到 Azure App Service，因为 Azure 不需要中等信任。</span><span class="sxs-lookup"><span data-stu-id="02c2a-354">Don't do this if you are deploying to Azure App Service, because Azure does not require medium trust.</span></span> <span data-ttu-id="02c2a-355">在本教程在 2012 年 2 月正在编写时使用此方法使你的应用程序在中等信任中运行会导致错误在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="02c2a-355">At the time this tutorial is being written in February, 2012, using this method to make your application run in medium trust will cause an error in Azure.</span></span>

<span data-ttu-id="02c2a-356">如果你正在使用 Entity Framework Code First 迁移，并且你要部署到的宿主提供程序在中等信任中运行你的应用程序，请确保您拥有版本 5.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="02c2a-356">If you are using Entity Framework Code First Migrations and you are deploying to a hosting provider that runs your application in medium trust, make sure that you have version 5.0 or later installed.</span></span> <span data-ttu-id="02c2a-357">在实体框架版本 4.3，迁移以更新数据库架构需要完全信任。</span><span class="sxs-lookup"><span data-stu-id="02c2a-357">In Entity Framework version 4.3, Migrations requires full trust in order to update the database schema.</span></span>

## <a name="http-40417-not-found-error"></a><span data-ttu-id="02c2a-358">找不到 HTTP 404.17 错误</span><span class="sxs-lookup"><span data-stu-id="02c2a-358">HTTP 404.17 Not Found Error</span></span>

### <a name="scenario"></a><span data-ttu-id="02c2a-359">方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-359">Scenario</span></span>

<span data-ttu-id="02c2a-360">你在 IIS 中的开发计算机上运行已部署的站点时，你将看到以下报表服务器无法处理 Default.aspx 的错误消息：</span><span class="sxs-lookup"><span data-stu-id="02c2a-360">When you run the deployed site on your development computer in IIS, you see the following error message reporting that the server can't process Default.aspx:</span></span>

<span data-ttu-id="02c2a-361">HTTP 错误 404.17-找不到</span><span class="sxs-lookup"><span data-stu-id="02c2a-361">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="02c2a-362">请求的内容似乎是脚本，因而将无法由静态文件处理程序。</span><span class="sxs-lookup"><span data-stu-id="02c2a-362">The requested content appears to be script and will not be served by the static file handler.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="02c2a-363">可能的原因和解决方案</span><span class="sxs-lookup"><span data-stu-id="02c2a-363">Possible Cause and Solution</span></span>

<span data-ttu-id="02c2a-364">你计算机上可能未安装 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="02c2a-364">ASP.NET 4.5 might not be installed on your computer.</span></span> <span data-ttu-id="02c2a-365">作为本系列中说明了如何安装 ASP.NET 4.5 中的测试环境教程，请参阅中部署到 IIS 的步骤。</span><span class="sxs-lookup"><span data-stu-id="02c2a-365">See the steps in the Deploying to IIS as a Test Environment tutorial in this series that explain how to install ASP.NET 4.5.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="02c2a-366">上一篇</span><span class="sxs-lookup"><span data-stu-id="02c2a-366">Previous</span></span>](deploying-extra-files.md)