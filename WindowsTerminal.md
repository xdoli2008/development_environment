# Windows Terminal

> [windows terminal](https://github.com/microsoft/terminal) 是今年微软Build大会上推出的一款的全新终端，用来代替cmder之类的第三方终端。具有亚克力透明、多标签、Unicode支持(中文,Emoji)、自带等宽字体等这些特性。

## 安装

>MicroSoft Store下载安装

![1](https://oos-cn-kirayoshikage.oss-cn-hangzhou.aliyuncs.com/images/20190901171122.png)

![2](https://oos-cn-kirayoshikage.oss-cn-hangzhou.aliyuncs.com/images/20190901171658.png)

## 美化

> [美化来源](https://gitee.com/dragondove/notes/blob/master/Misc/%E8%BD%AF%E4%BB%B6%E6%8E%A8%E8%8D%90.md)

```json
{
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "defaultProfile": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
    "profiles": [
        {
            // Make changes here to the powershell.exe profile
            "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
            "name": "Windows PowerShell",
            "commandline": "powershell.exe",
            "cursorShape": "emptyBox",
            "colorScheme": "Material Dark",
            "useAcrylic": true,
            "acrylicOpacity": 0.8,
            "fontFace": "Hack NF",
            "fontSize": 13,
            "startingDirectory":"./",
            "hidden": false
        },
        {
            // Make changes here to the cmd.exe profile
            "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
            "name": "cmd",
            "commandline": "cmd.exe",
            "hidden": false
        },
        {
            "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
            "hidden": false,
            "name": "Azure Cloud Shell",
            "source": "Windows.Terminal.Azure"
        }
    ],
    "schemes": [
        {
            "name": "Material Dark",
            "colors": [
                "#212121",
                "#b7141f",
                "#45dde4",
                "#f6981e",
                "#434ea2",
                "#560088",
                "#0e717c",
                "#efefef",
                "#656565",
                "#e83b3f",
                "#7aba3a",
                "#257fad",
                "#54a4f3",
                "#aa4dbc",
                "#26bbd1",
                "#d9d9d9"
            ],
            "foreground": "#e5e5e5",
            "background": "#171717"
        }
    ],
    "keybindings":[
        {
            "command":"copy",
            "keys":[
                "ctrl+c"
            ]
        },
        {
            "command":"paste",
            "keys":[
                "ctrl+v"
            ]
        },
        {
            "command":"newTab",
            "keys":[
                "ctrl+n"
            ]
        },
        {
            "command":"closeTab",
            "keys":[
                "ctrl+shift+w"
            ]
        },
        {
            "command":"splitHorizontal",
            "keys":[
                "alt+["
            ]
        },
         {
            "command":"splitVertical",
            "keys":[
                "alt+]"
            ]
        },
         {
            "command":"moveFocusUp",
            "keys":[
                "alt+up"
            ]
        },
         {
            "command":"moveFocusDown",
            "keys":[
                "alt+down"
            ]
        },
         {
            "command":"moveFocusLeft",
            "keys":[
                "alt+left"
            ]
        },
          {
            "command":"moveFocusRight",
            "keys":[
                "alt+right"
            ]
        },
          {
            "command":"resizePaneUp",
            "keys":[
                "ctrl+alt+up"
            ]
        },
          {
            "command":"resizePaneDown",
            "keys":[
                "ctrl+alt+down"
            ]
        },
          {
            "command":"resizePaneLeft",
            "keys":[
                "ctrl+alt+left"
            ]
        },
         {
            "command":"resizePaneRight",
            "keys":[
                "ctrl+alt+right"
            ]
        },
         {
            "command":"closePane",
            "keys":[
                "ctrl+w"
            ]
        },
         {
            "command":"switchToTab0",
            "keys":[
                "ctrl+1"
            ]
        },
         {
            "command":"switchToTab1",
            "keys":[
                "ctrl+2"
            ]
        },
        {
            "command":"switchToTab2",
            "keys":[
                "ctrl+3"
            ]
        },
        {
            "command":"switchToTab3",
            "keys":[
                "ctrl+4"
            ]
        },
        {
            "command":"switchToTab4",
            "keys":[
                "ctrl+5"
            ]
        },
        {
            "command":"switchToTab5",
            "keys":[
                "ctrl+6"
            ]
        },
        {
            "command":"switchToTab6",
            "keys":[
                "ctrl+7"
            ]
        },
        {
            "command":"switchToTab7",
            "keys":[
                "ctrl+8"
            ]
        },
          {
            "command":"scrollUp",
            "keys":[
                "ctrl+up"
            ]
        },
          {
            "command":"scrollUpPage",
            "keys":[
                "ctrl+shift+up"
            ]
        },
          {
            "command":"scrollDown",
            "keys":[
                "ctrl+down"
            ]
        },
          {
            "command":"scrollDownPage",
            "keys":[
                "ctrl+shift+down"
            ]
        }
    ]
}
```

## Tab自动补全

>首先，`notepad $PROFILE` 打开PowerShell自定义profile文件、输入代码 `Set-PSReadlineKeyHandler -Key Tab -Function MenuComplete`

```powershell
# 如果之前没有配置文件，就新建一个 PowerShell 配置文件
if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }
# 用记事本打开配置文件
notepad $PROFILE
```

## PoShFuck

[github](https://github.com/mattparkes/PoShFuck)

`管理员模式运行terminal`

> 输入错误的命令时，请输入 “ fuck”

```powershell
Set-ExecutionPolicy RemoteSigned
iex ((new-object net.webclient).DownloadString('https://raw.githubusercontent.com/mattparkes/PoShFuck/master/Install-TheFucker.ps1'))
```

`fuck`（别名Invoke-TheFuck）
这是命令，它合并了您的最后一个命令，并为您提供了修复它的选项。

`fuck!`（别名Invoke-TheFuck -Force）
此命令将执行建议的选项，而不会提示用户。

`WTF`（别名为Get-FuckingHelp）
Googles您的上一个控制台错误。

`Get-Fucked`
打印您以前使用PoShFuck进行更正的命令列表。

## 安装fzf

`管理员模式运行terminal`

### 首先安装fzf

```powershell
scoop install fzf
```

### 安装Powershell的fzf容器

```powershell
Install-Module PSFzf
```

### Profile中禁用默认按键 - 放在Import上面

```powershell
Remove-PSReadlineKeyHandler 'Ctrl+r'
```

### Profile中启用PSFzf

```powershell
Import-Module PSFzf
```

`Ctrl+r`
显示命令行记录、可检索

`Ctrl+t`
显示文件下所有文件、可检索

## 添加右键

### 创建图标文件夹

`C:\Users\你的用户名\AppData\Local 新建一个 Terminal 文件夹`

``` cmd
mkdir "%USERPROFILE%\AppData\Local\Terminal"
```

_其实建这个文件夹就是为了存放图标而已，理解后可以自己找一个地方放[图标](https://raw.githubusercontent.com/microsoft/terminal/master/res/terminal.ico)

### 添加注册表文件

>新建一个文件，文件名随意 比如我的：`addwt.reg`。记得保存为`.reg`文件

```powershell
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shell\wt]
@="Windows Terminal"
"Icon"="%USERPROFILE%\\AppData\\Local\\Terminal\\terminal.ico"

[HKEY_CLASSES_ROOT\Directory\Background\shell\wt\command]
@="C:\\Users\\[你的电脑用户名！你的电脑用户名！你的电脑用户名！]\\AppData\\Local\\Microsoft\\WindowsApps\\wt.exe"
```

>执行 reg 文件。发现右键菜单就多了一个 Windows Terminal here 的选项了！
