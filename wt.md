# Windows Terminal

[windows terminal](https://github.com/microsoft/terminal) 是今年微软Build大会上推出的一款的全新终端，用来代替cmder之类的第三方终端。具有亚克力透明、多标签、Unicode支持(中文,Emoji)、自带等宽字体等这些特性。

* [安装](###安装)
* [美化](###美化)
* [添加右键](###添加右键)

### 安装

MicroSoft Store下载安装

![](https://oos-cn-kirayoshikage.oss-cn-hangzhou.aliyuncs.com/images/20190901171122.png)

![](https://oos-cn-kirayoshikage.oss-cn-hangzhou.aliyuncs.com/images/20190901171658.png)

### 美化

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
            "fontFace": "Cascadia Code",
            "fontSize": 13,
            "startingDirectory": "./",
            "hidden": false
        },
        {
            // Make changes here to the cmd.exe profile
            "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
            "name": "cmd",
            "commandline": "cmd.exe",
            "hidden": false
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
    "keybindings": []
}
```

### 添加右键

#### 创建图标文件夹

`C:\Users\你的用户名\AppData\Local 新建一个 Terminal 文件夹`

``` cmd
mkdir "%USERPROFILE%\AppData\Local\Terminal"
```

_其实建这个文件夹就是为了存放图标而已，理解后可以自己找一个地方放[图标](https://raw.githubusercontent.com/microsoft/terminal/master/res/terminal.ico)

#### 添加注册表文件

新建一个文件，文件名随意 比如我的：`addwt.reg`。记得保存为`.reg`文件

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shell\wt]
@="Windows Terminal"
"Icon"="%USERPROFILE%\\AppData\\Local\\Terminal\\terminal.ico"

[HKEY_CLASSES_ROOT\Directory\Background\shell\wt\command]
@="C:\\Users\\[你的电脑用户名！你的电脑用户名！你的电脑用户名！]\\AppData\\Local\\Microsoft\\WindowsApps\\wt.exe"
```

执行 reg 文件。发现右键菜单就多了一个 Windows Terminal here 的选项了！










