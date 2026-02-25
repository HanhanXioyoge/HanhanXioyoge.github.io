---
title: '如何在Windows上配置Claude Code'
date: 2026-02-25
permalink: /posts/2026-02-25-install-claude-code-on-your-windows/
tags:
  - cool posts
  - category1
  - category2
---

> **导读**：随着 AI 辅助编程的深入，将强大的大模型能力直接集成到本地终端，已成为实现工作流自动化和提升研发效率的必由之路。Claude Code 作为一款优秀的命令行 AI 助手，能够极大地加速我们的代码开发与重构过程。不过，在 Windows 环境下从零配置它，往往需要避开一些环境配置的坑点。
> 
> 本文将提供一份极简、高效的 Windows 本地部署指南。全篇只需几分钟，带你快速完成环境搭建，立刻投入实战。

**在这篇文章中，我将带你走通以下核心流程：**

1. **环境筑基**：前往官方获取并正确安装基础运行环境 `Node.js`。
2. **终端部署**：调出 PowerShell，通过命令行全局安装 Claude。
3. **极速跳过**：分享一个实用的小技巧——如何跳过繁琐的初始登录验证。
4. **工具接管**：演示如何使用 `ccswitch` 轻松完成后续的配置与接管。

无论你是刚开始搭建 AI 编程环境的新手，还是追求极致自动化工作流的极客，这篇快速教程都能帮你省去查阅冗杂文档的时间，一步到位！

第一步：环境筑基 —— 为什么我们需要 Node.js？
======


很多新手在配置命令行 AI 助手时，往往会疑惑：**“我只是想用 Claude，为什么要先装一个叫 Node.js 的东西？”**

答案很简单：Claude Code 作为一个现代化的命令行工具（CLI），其底层是由 JavaScript 编写的，并作为 npm（Node Package Manager）包进行分发。
* **Node.js** 提供了让这些代码在你的 Windows 系统底层直接运行的环境。
* 随之附带的 **npm**，则是我们下载和安装 Claude Code 的“应用商店”。

**操作步骤：**
1. 前往 [Node.js 官方网站](https://nodejs.org/)。
   ![alt text](/images/blog/2026-02-25-install-claude-code-on-your-windows/image.png)
2. 下载推荐给大多数用户的 **LTS（长期支持版）** Windows 安装包。
3. 双击运行，**一路点击“Next”即可**（默认设置已经足够，不需要修改路径或勾选额外的高级选项）。

*提示：安装完成后，打开 PowerShell，输入 `node -v` 和 `npm -v`。如果能看到版本号输出，就说明我们的“地基”已经打好了！*

第二步：使用 PowerShell 安装 Claude code
======

准备好 Node.js 这个“底层地基”后，我们就可以正式拉取并部署 Claude Code 了。Anthropic 官方提供了一个非常现代化的 PowerShell 脚本，只需一行命令即可全自动完成安装。

**操作步骤：**

1. **唤醒终端**：按下 `Win` 键，搜索并打开 **PowerShell**。建议右键点击选择“以管理员身份运行”，这样可以最大程度避免后续执行过程中的系统权限拦截。
2. **执行安装命令**：将官方提供的以下命令复制、粘贴到你的 PowerShell 窗口中，然后按下回车键：
![alt text](/images/blog/2026-02-25-install-claude-code-on-your-windows/image-1.png)

    ```powershell
    irm https://claude.ai/install.ps1 | iex
    ```

第三步：配置环境变量 —— 让系统“认识” Claude 命令
======

很多朋友在看到安装成功的提示后，满心欢喜地在终端输入 `claude`，却被系统泼了一盆冷水，抛出红字报错：**“无法将 'claude' 项识别为 cmdlet、函数、脚本文件或可运行程序的名称”**。

别慌！这是由于 Windows 系统的“寻路机制”导致的。虽然 Claude Code 已经安稳地躺在你的硬盘里，但系统还不知道它的具体位置。我们需要手动将它的所在路径添加到系统的**环境变量**（Path）中。

**详细配置步骤：**

1. **查看 claude 的路径**：claude 路径通常位于 `C:\Users\<你的用户名>\.local\bin`。请用鼠标选中并右键复制这串路径。

    ![alt text](/images/blog/2026-02-25-install-claude-code-on-your-windows/image-2.png)
2. **进入 Windows 环境变量设置**：按下键盘上的 Win 键，直接输入搜索词 “环境变量”，点击 “编辑系统环境变量”，在弹出的“系统属性”窗口右下角，点击 “环境变量(N)...” 按钮。在弹出的窗口中，找到上半部分“用户变量”列表里的 Path 选项，双击打开它。点击右侧的 “新建” 按钮。将刚才复制的claude路径粘贴进去。依次点击所有打开窗口的 “确定” 按钮，保存设置并退出。
![alt text](/images/blog/2026-02-25-install-claude-code-on-your-windows/image-3.png)
3. **重启终端并验证（关键！）**：环境变量修改后，不会在当前已经打开的终端中立即生效。请务必关闭当前的 PowerShell 窗口。重新打开一个全新的 PowerShell 窗口，输入以下命令进行验证：

    ```powershell
    claude --version
    ```

    如果屏幕上成功输出了 Claude Code 的版本号（例如 `@anthropic-ai/claude-code/x.x.x`），恭喜你！你的 AI 编程助手已经被彻底唤醒，随时待命。


第四步：模型自由 —— 跳过官方登录，使用 `ccswitch` 接入任意大模型
======

> **💡 核心痛点**：由于严格的区域网络限制或缺乏 Anthropic 官方账号，很多国内开发者在使用原生 Claude Code 时，往往在第一步 `claude login` 的浏览器授权环节就被无情卡住。

作为一个追求效率的极客，我们怎么能被单一平台绑定？这时候，开源神器 **`ccswitch`** 就派上大用场了。它的核心原理是在本地建立一层代理拦截（Proxy），“欺骗”并接管 Claude Code 的网络请求。这样一来，你不仅能完美跳过强制登录，还能自由地将后端的算力替换为你手头的任何大模型（例如通过中转 API 接入 OpenAI、DeepSeek 等）。



**终极实操步骤：**

1. **绕过官方鉴权**：
修改用户目录配置文件，首先找到你系统用户目录下的 .claude.json 文件： Windows: C:\Users\<用户名>\.claude.json。然后添加跳过登录字段 在文件中加入以下内容（注意 JSON 格式正确）：
    ```json
    {
    "hasCompletedOnboarding": true
    }
    ```
    保存并重启 CLI 保存文件后重新启动 Claude Code CLI，即可跳过登录流程。

1. **获取 `cc-switch` 客户端**
目前社区中最成熟的方案是使用带图形化界面（GUI）的 `cc-switch` 桌面端。
   * 前往开源仓库 `farion1231/cc-switch` 的 [GitHub Releases 页面](https://github.com/farion1231/cc-switch/releases)。
   * 找到最新的 Windows 版本（安装包）下载并完成安装。
![alt text](/images/blog/2026-02-25-install-claude-code-on-your-windows/image-5.png)

1. **配置自定义 Provider（模型供应商）**
打开 `cc-switch` 软件，我们需要告诉它“该把数据转发给谁”：
   * 点击右上角加号添加新的 **Provider**。
   * 去对应的大模型官网获取对应的API key填充到下面。（以minmax为例）
![alt text](/images/blog/2026-02-25-install-claude-code-on-your-windows/image-4.png)

1. **见证奇迹的时刻**
现在，回到你的 PowerShell 终端，使用 `cd` 命令进入你想要编写代码的项目文件夹，然后自信地敲下：
    ```powershell
    claude
    ```
    ![alt text](/images/blog/2026-02-25-install-claude-code-on-your-windows/image-6.png)
    然后输入选择模型
    ```
    /model
    ```
    ![alt text](/images/blog/2026-02-25-install-claude-code-on-your-windows/image-7.png)


就这样我们完成了 Claude Code 的彻底部署与自定义接管！
------