# 软件环境

## Windows 软件 - 按顺序下载安装软件

### 包管理工具 - [Scoop](scoop.md)

[官网](https://scoop.sh/)

### 下载加速 - aria2

[官网](https://aria2.github.io/)

```powershell
# 通过 scoop 安装
scoop install aria2
```

### 版本管理 - git

[官网](https://gitforwindows.org/)

```powershell
# 通过 scoop 安装
scoop install git
```

### 压缩 && 解压缩工具 - bandizip

[官网](http://www.bandisoft.com/bandizip/)

```powershell
# 通过 scoop 安装 依赖 extras bucket
scoop install bandizip
```

### 快速搜索工具 - Everything

[官网](https://www.voidtools.com/)

```powershell
scoop install everything
```

### 快速启动工具 - Wox || Listary

[wox](http://www.wox.one/)

```powershell
scoop install wox
```

### 编辑工具 - VSCode && sublime

[vscode](https://code.visualstudio.com/) [sublime](https://www.sublimetext.com/)

```powershell
scoop install vscode
scoop install sublime-text
```

### 字体 - Hack-NF

```powershell
# powerline 字体可以通过在 scoop 里增加 nerd-fonts bucket 安装 nerd-fonts 来支持
scoop bucket add nerd-fonts
scoop install Hack-NF
```

### 屏幕显示按钮工具 - carnac

[github](https://github.com/Code52/carnac)

```powershell
scoop install carnac
```

### Markdown 编辑器 - Typora

[typora](https://typora.io/)

```powershell
scoop install typora
```

### 数据库工具 - Heidisql

[heidisql](https://www.heidisql.com/)

```powershell
scoop install heidisql
```

### 卸载工具 - Geek uninstaller

```powershell
scoop install geekuninstaller
```

### 视频播放器 - mpc-be

```powrshell
scoop install mpc-be
```

### 视频录制 / 直播工具 - OBS-studio

[官网](https://obsproject.com/)

```powershell
scoop install obs-studio
```

### 刻录工具 - Rufus

[官网](http://rufus.ie/)

```powershell
scoop install rufus
```

### 快速预览工具 - QuickLook

微软应用商店获取 uwp 版本，scoop 可以获取常规版本

```powershell
scoop install quicklook
```