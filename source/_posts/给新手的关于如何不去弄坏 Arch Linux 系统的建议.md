---
layout:     post
title:      "2025-03-11-Arch Linux 系统美化"
subtitle:   "Arch Linux 系统美化"
date:       2025-03-11 21:00:06
author:     "Nickwei"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 随笔
---



原始页面来自 [Debian Wiki](https://wiki.debian.org/zh_CN/DontBreakDebian)。

Arch Linux 是滚动更新的系统。从单独的时刻上去看，其即使可能会在更新后出现问题，但由于滚动更新，这些问题也可以被快速修复，因而总体上依然稳定可靠。除去上游引入的问题，用户手上持有的系统最高权限——[root](https://wiki.archlinuxcn.org/wiki/Root) 权限——也通常是导致系统损坏的导火索。背离通常的操作手段导致系统故障是正常的，因而我们在此处列出常见的导致系统故障的操作，以期帮助大家避免这些问题。不过，若有充分的知识和谨慎的操作，即使出了问题，通常也是可以妥当解决的。

在此之前，需要知道一点的是，来自[官方仓库](https://wiki.archlinuxcn.org/wiki/官方仓库)的软件包受到官方支持，且来自 `core` 仓库的软件包更是会先进行严格的审核。而在其他系统中，你**可能会从各个网站下载安装包，但无论在哪个系统上，这通常都伴随风险**。在 Arch Linux 上，还有很多第三方软件的安装脚本来自 [AUR](https://wiki.archlinuxcn.org/wiki/AUR)。这些脚本相较于用户手动使用命令编译安装来说，可以让通过脚本安装的软件受到本系统的包管理软件，[pacman](https://wiki.archlinuxcn.org/wiki/Pacman) 管理，这可以极大的减小自行安装与包管理冲突的风险，但这些脚本亦可能包含恶意代码（这曾经发生过，虽然不常见）。因此，请尽量选用来自官方仓库的软件包，并在使用来自 AUR 的安装脚本前对它们做仔细检查（比如检查包含的网址，可能包含的破坏性命令等）。

中文用户可能会选用来自[非官方用户仓库](https://wiki.archlinuxcn.org/wiki/非官方用户仓库)，[[archlinuxcn\]](https://wiki.archlinuxcn.org/wiki/Archlinuxcn) 的软件包。同样，你也应该谨慎选用这些软件包，在非官方软件包出问题时也请向相应的人员报告问题。

## 01. 数据无价，分区操作需谨慎

根据[安装指南#分区方案示例](https://wiki.archlinuxcn.org/wiki/安装指南#分区方案示例)，您可能会将除 `/boot` 和 `swap` 之外的所有系统所需内容（这包括 `/home`，您的很多个人数据会存储在这里）放在一个单独的分区。这样的配置对新用户相对友好，但是在您进行某些可能会损害数据的操作（如调整磁盘分区大小）时，由于个人数据和系统文件存放在同一个分区内，若是因为相关操作导致分区损毁，则您很可能会同时失去珍贵的个人数据。

因此，分区操作需谨慎，在安装系统的时候就应当通盘考虑如何分配磁盘，因为稍后再修改所要花费的精力会更大。比如，参考“不要把鸡蛋放在同一个篮子里”的道理，您可以在安装时，将一些目录（如 `/home`）作为单独的挂载点，将这些目录下的内容放在其他分区。这样，即使系统分区出了问题，您的数据也在其他分区内完好无损，并且您可以快速恢复您的工作环境。具体请参阅 [fstab](https://wiki.archlinuxcn.org/wiki/Fstab)。

## 02. 不要混用测试仓库

如果你使用桌面环境，你有可能想提前尝试测试版本的桌面环境，比如 [KDE](https://wiki.archlinuxcn.org/wiki/KDE) 和 [GNOME](https://wiki.archlinuxcn.org/wiki/GNOME)，并相应启用 `gnome-unstable` 和 `kde-unstable`。需要注意的是，这些仓库需要同时与[测试仓库](https://wiki.archlinuxcn.org/wiki/官方仓库#testing_仓库)，也就是 `core-testing` 和 `extra-testing` 同时启用（如果有启用更多的官方仓库也要启用相应的测试仓库），否则可能导致[部分升级](https://wiki.archlinuxcn.org/wiki/部分升级)，简单来说就是新旧软件包不兼容的情况。要提前尝试，就都要提前尝试。一旦产生错误，则必须尽快解决问题。

通常，只要 pacman 可以运行，完整地启用测试仓库后，进行 `pacman -Syu` 就能修复这些问题。

## 03. 不要“下载”显卡驱动

显卡制造商的官网可能会提供显卡驱动的安装脚本，**但是也请用来自软件仓库的驱动软件包**。Arch Linux 的软件仓库已经（基本上）提供了这些驱动，并且可以伴随 Linux 内核升级而升级，这比单独的安装脚本要可靠和安全得多。通常情况下，查阅 [OpenGL](https://wiki.archlinuxcn.org/wiki/OpenGL)、[Vulkan](https://wiki.archlinuxcn.org/wiki/Vulkan) 以及 [VA-API](https://wiki.archlinuxcn.org/wiki/VA-API) 这三个 wiki 页面足以引导你安装并配置好运行桌面所需的显卡驱动。

即使是臭名昭著的 [NVIDIA](https://wiki.archlinuxcn.org/wiki/NVIDIA)，近年来的表现也在逐渐稳定。要查阅与具体硬件品牌相关的更多信息，请参考 [NVIDIA](https://wiki.archlinuxcn.org/wiki/NVIDIA)、[AMDGPU](https://wiki.archlinuxcn.org/wiki/AMDGPU)、[Xorg#AMD](https://wiki.archlinuxcn.org/wiki/Xorg#AMD) 或 [Intel 图形处理器](https://wiki.archlinuxcn.org/wiki/Intel_图形处理器)等文。本 wiki 同时提供其他软件在 Arch Linux 上的使用说明，其中也可能包含相关软件在与特定显卡配合使用时需要单独采取的措施。

## 04. 小心 `make install` 和其他类似命令

[pacman](https://wiki.archlinuxcn.org/wiki/Pacman) 包管理通过统一的方式管理系统软件及其文件，但 `make install`、`ninja install` 等安装的文件不受 pacman 管理，且可能与 pacman 管理的文件相冲突。同样，如果需要卸载由这些命令安装的文件，也需要花费一番功夫。

同样，直接运行这些命令会需要你自行管理这些软件的升级等，事实上十分不便。来自 [AUR](https://wiki.archlinuxcn.org/wiki/AUR) 的安装脚本实际上采用与软件仓库打包相一致的过程，因而这样安装的软件受到pacman管理。在了解相应风险后，您也可以使用 [AUR 助手](https://wiki.archlinuxcn.org/wiki/AUR_助手)帮助你升级来自 [AUR](https://wiki.archlinuxcn.org/wiki/AUR) 的软件包。如果AUR也实在没有，也可以考虑自己[创建软件包](https://wiki.archlinuxcn.org/wiki/创建软件包)（当然这并不轻松），让 pacman 管理。还有一些常见的类似建议列在下方。

1. 不要直接 `pip install`

   [Python](https://wiki.archlinuxcn.org/wiki/Python) 有相当多的库并不在 Arch Linux 仓库内，如果你不想使用 [Arch 构建系统](https://wiki.archlinuxcn.org/wiki/Arch_构建系统)亲自打包 Python 程序的话，使用 `pip install` 是个折中的办法。但是，**请一定在 venv（或类似的虚拟环境）中运行**。如果你 `# pip install`，那么你安装的文件会与 pacman 管理的文件产生冲突。然而，即使使用 `pip install --user` 将程序安装到 `~/.local` 下，也可能安装了与系统软件包重复但版本不同的库，从而导致系统上安装的某些依赖该 Python 库的程序因库版本不正确而出错。

   如果你需要用的 Python 程序支持用命令行启动运行，而无需在 Python 代码中 `import` 调用的话，推荐使用 [python-pipx](https://archlinux.org/packages/?name=python-pipx)包 来安装它。pipx 会自动为你创建 venv，并自动在 venv 中安装你需要的程序。

   有时候一些 Python 程序会依赖一些重量级库，比如 PyQt/PySide/PyGObject 等，如果在 venv 这样的隔离环境中安装则需要在 venv 中安装所需的 [Qt](https://wiki.archlinuxcn.org/wiki/Qt)/glib 库，这通常无法与系统上的其它软件良好集成。这种时候，你可以用 `python -m venv --system-site-packages` 来创建 venv 并在其中安装你需要的软件包。这样创建的 venv 不是与系统环境完全隔离的，venv 之内的 Python 能够导入系统范围安装的包，而系统环境的包则看不到 venv 内的包，因此不会干扰系统软件包正常工作，相当于获得了 `pip install --user` 的优点而规避了它的缺点。

2. 不要默认启用 anaconda 环境

   [anaconda](https://wiki.archlinuxcn.org/wiki/Python#软件包管理) 是个不错的管理 Python 软件的方式。然而，它自带了包括 curl 和 ncurses 在内的许多库文件，其版本可能与系统所需要的版本冲突。因此，请不要默认启用 anaconda 环境，仅在需要使用的时候启用。

## 05. 不要盲从教程

标题不是在说不要看任何教程，而是说，应该同时比对几份同主题的教程（对于 ArchWiki，则也可以是中英文，甚至其他语言），以及参考说明文档。同样，教程也有时效性，如果是五年前的教程，可能现在已经完全不适用。

但，**无论是在跟随教程之前，还是在对比几份教程之前，都应该搞清楚教程中的命令到底会做出哪些操作**。这样可能会帮助你及时发现错误，当然，即使未能发现，也能更迅速地帮助你恢复系统正常。

除了 ArchWiki 外，[man](https://wiki.archlinuxcn.org/wiki/Man) 命令等是已经存在于你系统上的文档。这些也是参考来源。

## 06. 不要盲目照抄配置文件与脚本

盲目照抄配置文件和脚本对于系统的危害是深远且多方面的。

每个系统或应用都有其独特的运行环境和需求。盲目照抄配置文件、脚本，往往忽略了这些差异，可能导致配置不兼容，进而引发系统错误或崩溃。

当您使用别人提供的脚本时，应当知道它是用来做什么的、它依赖什么软件包、它应当被何 [shell](https://wiki.archlinuxcn.org/wiki/Shell) 执行等。

[点文件](https://wiki.archlinuxcn.org/wiki/Dotfiles#用户仓库)一文中提到的其他用户提供的配置文件、各大代码托管平台上的用户点文件仓库以及 [AUR](https://wiki.archlinuxcn.org/wiki/AUR) 中类似于 [ml4w-hyprland](https://aur.archlinux.org/packages/ml4w-hyprland/)AUR 的包，都是针对那些用户自身，而非您的习惯或设备来设计的。比如说，假如您喜欢某人的终端增强配置，就草率地将其 `~/.bashrc` 直接抄进了您的 `~/.config/fish/config.fish`，这样的话，出现问题时，无论是您要向社区询问，还是他人试图解决您的问题，都会因为这其中积累的无数个“未知”，给您自己和社区带来莫大的麻烦。

## 07. 移除软件包需谨慎

软件包之间有依赖关系，也就是一个软件包必须和另一些软件包一起存在。因此，移除一个软件包可能会需要相关的其他软件包也被一同移除。

移除软件包前，pacman 会显示要移除的包的列表。**一定要仔细查看每个即将被删除的包**，它们有的可能是你仍需要使用的软件包。如果不清楚，除了询问其他人以外，你还可以通过 [pacman 的查询命令](https://wiki.archlinuxcn.org/wiki/Pacman#查询包数据库)来查看每个软件包的简介与相关信息。

## 08. 记得自己做过什么

记得自己做过什么在出问题的时候可以帮助你或者是让其他人帮你快速解决问题。比如，改动配置文件时，也许可以原地留一下注释和日期，标注原因，之类的。本文先前所提及的“不要照抄其他配置文件”也是同理，充分把握自己的系统这件事对解决之后可能发生的问题而言十分重要。

总的来说，要维持 Arch Linux 系统的稳定，你自然要付出一定的精力。

## 09. 谨慎对待 LLM 给出的内容

[LLM](https://en.wikipedia.org/wiki/Large_Language_Model)，大型语言模型（也就是 OpenAI 的 ChatGPT，Anthropic 的 Claude，Google 的 Gemini，深度求索的 DeepSeek 等 “AI”），看似是人类可以向 AI 询问任何问题，AI 就会给出看着非常可信的答案。有人可能会觉得如获至宝，看到有人问问题就把问题丢给它们问，再把回答随便贴上去。

但是，现阶段的通用大型语言模型，即便是在有联网工具能力的情况下（比如 ChatGPT 的搜索模式），也只能基本确保它们组出的是**语法语气没有问题**的句子，而**不是事实正确**的句子。即便是现在推理用的大模型，也并**没有对现实的认知能力**，自然没有其他社区成员的经验，询问它们是不大可能获得诸如“你电脑在更新的时候大写锁定键忽然闪灯，是因为闭源 NVIDIA 驱动和内核互作导致更新时内核崩溃，根据你的显卡型号，你应该换用 [nvidia-open](https://archlinux.org/packages/?name=nvidia-open)包 这个包”之类的详细结果的。

好吧，LLM 似乎确实不适合询问莫名其妙的疑难杂症——那如果是让它帮我写一个特定用途的小工具呢？不是说它们很擅长写电脑程序吗？

在你准备问出更多问题之前，再次强调一遍：**现阶段的 AI 没有对现实的认知能力**，它不能保证自己写的符合你的要求，甚至可能因为阴差阳错写出有害的东西出来（虽然更多时候是前者）。

因此，总结一下：如果一段文字看着是 AI 生成的，或者你打算向 AI 问问题，**请先认为你看到的内容一个字都不能信**。也请不要把“它说的对不对啊”的工作推给别人，因为比起对 LLM 缝缝补补，人类自己早就能把问题解决掉了。

## 10. 寻求他人帮助

Arch Linux 用户通常对 Arch Linux 上的问题更为熟悉。在遵循[行为准则](https://wiki.archlinuxcn.org/wiki/行为准则)的前提下，向[官方社区](https://wiki.archlinuxcn.org/wiki/首页#相关链接)和非官方的[国际社区](https://wiki.archlinuxcn.org/wiki/国际社区)（中文用户可以看看 [Arch Linux 中文社区](https://wiki.archlinuxcn.org/wiki/Arch_Linux_中文社区)）通常是个好主意。

[行为准则#常识](https://wiki.archlinuxcn.org/wiki/行为准则#常识)有言：

- 使用 Arch Linux，先要接受 [Arch 之道](https://wiki.archlinuxcn.org/wiki/Arch_之道)
- 先看文档，搜索网站，做好功课，再行提问
- 寻求帮助，耐心委婉
- 乐于奉献，止于损害

遵循基本前提，提供尽可能多的细节，保持耐心多等待，不要宣泄情绪。

当然，每个社区都会有自己的建议。但通常，使用即时通讯软件时，不要频繁换行发言，尽可能一次发完。上传日志建议使用外部网站（比如 [Pastebin](https://en.wikipedia.org/wiki/Pastebin) 和每个群组自行设置的类 Pastebin 网站），并且注意删掉私人信息。询问问题时待在有问题的设备前，不要“离线提问”，避免在他人给出建议的时候你却“暂时给不出日志”又或是“暂时摸不到电脑”而消耗其他社区用户的耐心。

最后，祝你的 Arch Linux 使用之旅顺利且愉快！









