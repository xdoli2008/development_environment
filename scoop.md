# scoop

[[官网]](https://scoop.sh)    [[github]](https://github.com/lukesampson/scoop)    [[wiki]](https://github.com/lukesampson/scoop/wiki)

>## [scoop开发软件安装](scoop-software.md)

## 安装

```powershell
# 将执行权限改为本地无需签名
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
# 下载并执行脚本 下面有安装到其他盘的教程
iwr -useb get.scoop.sh | iex
```

## 常用指令

```powershell
# 帮助
scoop help
# 搜索安卓相关软件
scoop search android
# 安装 git
scoop install git
# 给所有用户安装 git
sudo scoop install git --global # 需要先安装 sudo
# 卸载 git
scoop uninstall git
# 更新所有软件
scoop update *
# 查看 Android Studio 的软件信息
scoop info android-studio
# 删除软件的老版本
scoop cleanup
# 列出已安装的名字中带有 adopt 的软件
scoop list adopt # 不填写则列出所有已安装软件
# 切换软件版本
scoop reset python27
```

## 添加软件源

```powershell
# 添加软件源功能依赖于 git，请确保电脑中已经安装 git 并且配置好了环境变量（也可以使用 scoop 安装 git）
# 列出官方已知软件源
scoop bucket known
# 添加额外软件源
scoop bucket add extras # 推荐添加这个软件源，大部分软件都再这个源里
# 添加官方未知软件源
scoop bucket add name gitrepo # name 处填写自定义的名字，gitrepo 处填写 git 地址
```

## 问题记录

1. Q: 安装 scoop 的过程中网络连接错误，重新执行安装指令显示已经安装

   A: 删除 `%USERPROFILE%\scoop` 这个文件夹。

2. Q: 使用 scoop 安装软件时下载失败，重新执行安装指令显示已安装

   A: 先执行 scoop uninstall <软件名>，再次执行安装指令即可

3. Q: 如何安装软件到其他路径下

   A:

   ```powershell
   # 设置 scoop 安装路径为 D:\scoop
   $env:SCOOP='D:\scoop'
   [environment]::setEnvironmentVariable('SCOOP',$env:SCOOP,'User')
   # 安装 scoop
   iwr -useb get.scoop.sh | iex

   # 全局安装路径修改
   $env:SCOOP_GLOBAL='D:\apps'
   [environment]::setEnvironmentVariable('SCOOP_GLOBAL',$env:SCOOP_GLOBAL,'Machine')
   scoop install -g <app>
   ```

4. Q: 如何回退软件版本

   A: 我暂时没有在文档中找到回退版本相关的指令。

## 附录：scoop 文件夹结构

- scoop
  - apps # 软件文件夹，所有非全局安装的软件都在这
    - appname/current # 当前软件版本对应的文件夹的软链接，如果你对某个软件设置调用该文件夹下的软件（例如 maven 环境设为 current 目录，那么这个指向的软件永远都会是最新版本）
  - buckets # 软件源文件夹，所有软件的下载地址等元数据都保存在这里，内部文件夹都是由 git 形成的，因此也可以采用 git pull 来更新源。
  - cache # 软件安装包所在位置，如果遇到软件下载缓慢的情况，也可以用其他工具下载对应软件，然后修改文件名放置到这个目录下进行安装。
  - persist # 永久配置文件夹，大部分的软件的配置都会存到这个目录下，以保证软件最新版用的都是原来的配置。
  - shims # 软件二进制的超链接，基本所有的命令行工具都会在这个文件夹内建立一个超链接，目的是为了防止环境变量 PATH 受到过多污染。
