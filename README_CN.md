# 特别说明

这是一个fork版本，原地址是：https://github.com/daipeihust/im-select  
im-select是通过切换区域语言(Language)来切换输入法的。不能切换输入法的模式。实际使用中有两个问题：

* 需要在windows系统里添加英文键盘。
* 使用搜狗时，当从英文切换回中文输入法时，输入法的模式不会切换回中文输入法，而是保持英文输入法。
这里有一个[改进版](https://github.com/PEMessage/im-select-imm)，可以切换输入法的中英文模式（conversion mode）， 但是搜狗输入法不知道为什么不能切换
* 原工程里im-select-mspy是im-select中的另一个改进，使用模拟按键输入的方式切换。但是不能判断当前是否是中文输入法

# 概述
im-select可以让你从命令行切换输入法。这个项目是 [VSCodeVim](https://github.com/VSCodeVim/Vim) 的附属项目，VSCodeVim的自动切换输入法功能需要用到这个项目中的程序。

# 如何安装

## macOS

#### Homebrew

```shell
brew tap daipeihust/tap
brew install im-select
```

或者将下面一行复制到你的命令行中并运行：

```shell
curl -Ls https://raw.githubusercontent.com/daipeihust/im-select/master/install_mac.sh | sh
```
im-select程序会被下载到`/usr/local/bin/`路径。

## windows

下载 [im-select.exe](https://github.com/boostmerlin/im-select/blob/main/win/im-select/x64/Release/im-select.exe)，然后把它移动到一个合适的路径。
## linux

Linux环境下你不需要下载im-select，因为Linux有许多命令行工具可以切换输入法。


# Usage

## macOS
如果你的 PATH 包含 `/usr/local/bin`，你可以直接使用 `im-select`。

### 获取当前使用的输入法
```shell
/usr/local/bin/im-select
```
### 切换输入法
```shell
/usr/local/bin/im-select imkey
```
举例： `/usr/local/bin/im-select com.apple.keylayout.US`

## linux

### ibus

[@mengbo](https://github.com/mengbo) 为 ibus 提供了如下配置：

```
"vim.autoSwitchInputMethod.enable": true,
"vim.autoSwitchInputMethod.defaultIM": "xkb:us::eng",
"vim.autoSwitchInputMethod.obtainIMCmd": "/usr/bin/ibus engine",
"vim.autoSwitchInputMethod.switchIMCmd": "/usr/bin/ibus engine {im}"
```

### xkb-switch

[@VEL4EG](https://github.com/VEL4EG) 为 xkb-switch 提供了如下配置：

```
"vim.autoSwitchInputMethod.enable": true,
"vim.autoSwitchInputMethod.defaultIM": "us",
"vim.autoSwitchInputMethod.obtainIMCmd": "/usr/local/bin/xkb-switch",
"vim.autoSwitchInputMethod.switchIMCmd": "/usr/local/bin/xkb-switch -s {im}"
```

### fcitx

[@yunhao94](https://github.com/yunhao94) 为 fcitx 提供了如下配置：

```
"vim.autoSwitchInputMethod.enable": true,
"vim.autoSwitchInputMethod.defaultIM": "1",
"vim.autoSwitchInputMethod.obtainIMCmd": "/usr/bin/fcitx-remote",
"vim.autoSwitchInputMethod.switchIMCmd": "/usr/bin/fcitx-remote -t {im}",
```
### gdbus

[@d-r-q](https://github.com/d-r-q) 为 gdbus 提供了如下配置：

Put `gdbus call --session --dest org.gnome.Shell --object-path /org/gnome/Shell --method org.gnome.Shell.Eval "imports.ui.status.keyboard.getInputSourceManager().currentSource.index" | awk -F'[^0-9]*' '{print $2}'` into get-im.sh.

Put `gdbus call --session --dest org.gnome.Shell --object-path /org/gnome/Shell --method org.gnome.Shell.Eval "imports.ui.status.keyboard.getInputSourceManager().inputSources[$1].activate()"` into set-im.sh.

```
"vim.autoSwitchInputMethod.enable": true,
"vim.autoSwitchInputMethod.defaultIM": "0",
"vim.autoSwitchInputMethod.obtainIMCmd": "<path to get-im.sh>",
"vim.autoSwitchInputMethod.switchIMCmd": "<path to set-im.sh> {im}",
```

## windows
在Windows环境下，im-select.exe 是一个命令行工具，但是不能在系统的 cmd 或者 powershell 中运行，这是微软的bug，键盘的 API 不支持这两个命令行，我推荐你使用 git-bash。

> 注意：git-bash 并不是必须的，只有你在 VSCodeVim 的配置过程中，不知道当前的输入法的key，你才需要这样去获取输入法的key。

### 获取当前输入法的key
```shell
/path/to/im-select.exe
```

### 切换输入法
```shell
/path/to/im-select.exe locale
```

> 注意：Windows系统的路径和Linux会有些不一样，类似这样: C:\Users\path\to\file
