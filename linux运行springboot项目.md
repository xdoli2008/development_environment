# linux运行springboot项目

## 方法一

> 进入项目目录

```bash
cd /usr/webapp/erp
```

> 杀死项目进程

```bash
kill -9 $(ps -ef | grep erp-web | grep -v grep | awk '{print $2}')
```

> 运行项目

```bash
nohup java -jar erp-web-1.0.jar >log.txt &
```

> 查看日志

```bash
tail -f log.txt
```

## 方法二

> 进入项目目录

```bash
cd /usr/webapp/erp
```

> 创建脚本

```bash
vi boot.sh
```

> 编辑脚本

```bash
vim boot.sh
```

```bash
#! /bin/bash
#这里可替换为你自己的执行程序，其他代码无需更改
APP_NAME=erp-web.jar

#使用说明，用来提示输入参数
usage() {
    echo "Usage: sh 执行脚本.sh [up|log|start|stop|restart|status]"
    exit 1
}

#检查程序是否在运行
is_exist(){
  pid=`ps -ef|grep $APP_NAME|grep -v grep|awk '{print $2}' `
  #如果不存在返回1，存在返回0     
  if [ -z "${pid}" ]; then
   return 1
  else
    return 0
  fi
}

#启动方法
start(){
  is_exist
  if [ $? -eq "0" ]; then
    echo "${APP_NAME} is already running. pid=${pid} ."
  else
    nohup java -jar $APP_NAME > log.txt &
  fi
}

#停止方法
stop(){
  is_exist
  if [ $? -eq "0" ]; then
    kill -9 $pid
  else
    echo "${APP_NAME} is not running"
  fi  
}

#输出运行状态
status(){
  is_exist
  if [ $? -eq "0" ]; then
    echo "${APP_NAME} is running. Pid is ${pid}"
    tail -f log.txt
  else
    echo "${APP_NAME} is NOT running."
  fi
}

#重启
restart(){
  stop
  start
}

#根据输入参数，选择执行对应方法，不输入则执行使用说明
case "$1" in
  "start")
    start
    ;;
  "stop")
    stop
    ;;
  "status")
    status
    ;;
  "log")
    status
    ;;
  "restart")
    restart
    ;;
  "up")
    restart
    ;;
  *)
    usage
    ;;
esac
```

> 设置文件编码

```bash
vim boot.sh
:set ff=unix
:wq
```

> 添加脚本执行权限

```bash
chmod +x boot.sh
```

> 运行脚本

```bash
#重启项目
./boot.sh up

#查看项目日志
./boot.sh log

#终止项目
./boot.sh stop

#启动项目
./boot.sh start
```
