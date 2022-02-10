---
title: "在 M1 芯片 Mac 上使用 Homebrew"
date: "2020-12-07"
categories: 
  - "post"
tags: 
  - "apple-silicon"
  - "macos"
---

Homebrew 是 Mac 上管理软件包的最实用工具之一。但截至目前，它还没有对搭载 Apple silicon 的新 Mac 机型完成适配。根据维护者在 GitHub 上发布的[说明](https://github.com/Homebrew/brew/issues/7857#issue-647960270)，Homebrew 正在积极适配新架构的过程中，但目前还面临一些较大障碍，如缺少基于 ARM 架构的持续集成框架、很多软件包依赖的框架或编译器（`go`、`gcc`、`qt`）未适配等。

但是，Homebrew 目前在新 Mac 上仍然是可用的，并且已经发布了原生支持 ARM 架构的试验性版本。本文总结我在设置过程中探索出可行、相对实用的做法。

概括而言：

- 在不同路径分别安装针对 X86 和 ARM 架构的两个 Homebrew 版本；
- 优先使用 ARM 版 Homebrew 安装软件包，用 X86 版 Homebrew 安装尚未支持新平台的命令行软件；
- 使用 Homebrew Bundle 功能从旧 Mac 或 X86 版 Homebrew 迁移软件包。

后文将展开说明具体步骤。由于 ARM 版 Homebrew 仍然处于早期开发阶段，且我对终端环境下系统管理的了解相对粗浅，文章内容难免存在过时或不准确之处，请不吝指正。

### 1\. 安装 ARM 版 Homebrew

根据官方规划，ARM 版 Homebrew 必须安装在 `/opt/homebrew` 路径下，而非此前的 `/usr/local/Homebrew`。由于官方的安装脚本还未更新，可以通过如下命令手动安装：

```
cd /opt # 切换到 /opt 目录
mkdir homebrew # 创建 homebrew 目录
curl -L https://github.com/Homebrew/brew/tarball/master | tar xz --strip 1 -C homebrew
```

（**注：** 如果安装和使用过程中报错，可能是因为当前用户对于 `/opt/homebrew` 路径没有权限。对此，可以通过 `sudo chown -R $(whoami) /opt/homebrew` 接管该目录。）

虽然上面的步骤已经安装了 ARM 版 Homebrew，但此时在终端中运行 `brew` 命令并不能直接启动该版本。这是因为默认情况下，ARM 版 Homebrew 用来安装程序的路径 `/opt/homebrew/bin` 并不在环境变量 `PATH` 中，因此终端无法检索到该路径下的 `brew` 程序。

为此，编辑配置文件 `~/.zshrc`，加入如下内容：

```
path=('/opt/homebrew/bin' $path)
export PATH
```

（**注：** 本文推定读者使用 macOS Big Sur 的默认终端 zsh，如使用 bash 或 fish，则修改 `~/.bashrc` 或 `~/.config/fish/config.fish`，后同。）

然后重新启动终端。这样，直接执行 `brew` 就可以启动 ARM 版的 Homebrew 了。

* * *

#### 跑题：为什么 ARM 版 Mac 要使用 `/opt` 路径？

根据《文件系统层次结构标准》（[Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)，主要为 Linux 系统制定，但对具有共同 UNIX 基因的 macOS 也有参考价值）：

- [`/usr/local`](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/ch04s09.html) 目录用于系统管理员在本地安装软件。系统软件更新时，该目录应免于被覆盖。
- [`/opt`](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/ch03s13.html) 目录留作附加应用程序（add-on application）软件包的安装。安装在该目录下的软件包必须将其静态文件放置在单独的 `/opt/<package>` 或 `/opt/<provider>` 路径下。

历史上，`/usr/local` 主要用于放置在本地编译并另行安装的程序，避免和 `/usr` 下的系统自带版本冲突；而 `/opt` 则用于安装非系统自带的、第三方预先编译并发行的独立软件包。

显然，在如今的 macOS 使用场景下，用户很少会需要自行编译软件包，`/usr/local` 和 `/opt` 的区分一定程度上已经成为名义上的了。Homebrew 启用 `/opt` 作为 ARM 版的安装路径，可能更多是出于确保与 X86 版相互区隔的考虑。

* * *

### 2\. 安装 X86 版 Homebrew

如上所述，由于很多软件包目前还没有适配 ARM 架构（可以在 [Homebrew 的 Apple silicon issue 页面](https://github.com/Homebrew/brew/issues/7857)查询），无法通过 ARM 版 Homebrew 安装，因此我们还需要安装一份 X86 版的 Homebrew 备用。

X86 版 Homebrew 无法在 ARM 环境下安装。为此，需要先启动一个 X86 环境的终端。网络上[传播较广](https://osxdaily.com/2020/11/18/how-run-homebrew-x86-terminal-apple-silicon-mac/)的方法是创建一个 Terminal.app 的副本，然后令其在 Rosetta 兼容模式下运行，显得有些麻烦。

其实，注意到在任何命令前增加 `arch -x86_64`，就可以以 X86 模式运行该命令。因此，运行：

```
arch -x86_64 $SHELL
```

就可以启动一个 X86 模式终端，使得之后运行的命令都在 X86 模式下运行。

此时，运行 Homebrew 的官方安装脚本

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

就可以完成 X86 版 Homebrew 的安装。

### 3\. ARM 和 X86 版 Homebrew 的共存问题

经过上面的步骤，系统中目前有了两个 `brew` 程序，即 X86 版的 `/usr/local/bin/brew` 和 ARM 版的 `/opt/homebrew/bin/brew`。那么，当在终端中执行 `brew` 命令时，系统会以哪个为准呢？

当存在重名程序时，终端会按照重名程序在环境变量 `PATH` 中的先后顺序选择要执行的版本。由于之前配置 `~/.zshrc` 时，将 ARM 版 Homebrew 的路径放在了 `PATH` 的最前面，因此执行 `brew` 时，位于 `/opt/homebrew/bin/brew` 的 ARM 版将被优先运行。如果要运行 X86 版，则需要手动输入完整路径 `arch -x86_64 /usr/local/bin/brew`。

如果觉得输入这么长的命令过于麻烦，可以在 `~/.zshrc` 中为两个版本分别设置简称（alias）：

```
abrew='/opt/homebrew/bin/brew' # ARM Homebrew
ibrew='arch -x86_64 /usr/local/bin/brew' # X86 Homebrew
```

这样，执行 `abrew install <package>` 就可以调用 ARM 版 Homebrew 安装软件包，执行 `ibrew install <package>` 就可以调用 X86 版，从而不容易混淆。

至于应该使用哪个版本的 Homebrew 安装软件包，需要区别考虑：

- 对于**命令行（CLI）程序**：可以**优先尝试使用 ARM 版 Homebrew 安装**，保证获得针对新架构编译的版本，实现最佳的运行效果。但注意：
    - 有的软件包已经兼容新架构、但还没有发布相应的编译版，需要安装的过程中在本地编译，耗时会相对很长；
    - 如果软件包还没有兼容新架构，使用 ARM 版 Homebrew 安装会报错，此时可以换用 X86 版 Homebrew 安装。
- 对于**图形界面（GUI）程序**，即通过 Homebrew Cask 安装的 `.app` 程序：对于这类软件，Homebrew 起的作用只是从官方渠道下载这些软件的安装包，然后安装到 `/Applications` 路径（及执行安装脚本，如果有）。因此无论其是否针对新架构优化，通过任一版本 Homebrew 都可以安装。考虑到日后维护方便，建议**直接用 ARM 版 Homebrew 安装**即可。

### 4\. 从旧 Mac（或 X86 版 Homebrew）迁移软件包

如果你在拿到 M1 版 Mac 以后，选择了从旧 Mac 迁移数据、或恢复 Time Machine 备份，那么系统中可能已经有了遗留的 X86 版 Homebrew 和用它安装的软件包。此外，你可能也希望将以往惯用的软件包无遗漏地迁移到新 Mac。这些情况下，可以使用 Homebrew Bundle 功能辅助迁移工作。

要导出使用 X86 版 Homebrew 安装的软件包列表，运行：

```
/usr/local/bin/brew bundle dump
```

就能在当前目录下得到一个名为 `Brewfile` 的备份文件。该文件可以用普通文本编辑器打开，列举了所有已安装软件包、添加的第三方软件源（tap）、Homebrew Cask 管理的 GUI 程序和 [mas-cli](https://github.com/mas-cli/mas) 管理的 Mac App Store 程序：

```
tap "homebrew/bundle"
tap "homebrew/cask"
[…]
brew "dash"
brew "ffmpeg"
[…]
cask "bartender"
cask "bettertouchtool"
[…]
mas "Apple Configurator 2", id: 1037126344
mas "Aviary", id: 1522043420
[…]
```

记下 Brewfile 的路径。然后，使用 ARM 版 Homebrew 导入其内容并安装：

```
/opt/homebrew/bin/brew bundle --file /path/to/Brewfile
```

就完成了迁移。

需要注意的是，如果你是在同一台机器的两版 Homebrew 间迁移，那么并不需要迁移通过 Homebrew Cask 和 App Store 安装的 GUI 程序（Homebrew 也不会允许覆盖安装）。这时，可以手动编辑上述 `Brewfile`，将以 `cask` 和 `mas` 开头的记录删除，然后再通过 `brew bundle` 导入。

如果想让 ARM 版 Homebrew 接管已经安装的 Homebrew Cask 软件，只要将位于 `/usr/local/Caskroom` 下的各文件夹移动到 `/opt/homebrew/Caskroom` 即可：

```
mv /usr/local/Caskroom/* /opt/homebrew/Caskroom
```
