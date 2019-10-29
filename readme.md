# CentOS 8配置ss流程

1.用root用户登录  

2.用pip安装shadowsocks，执行命令

> pip3 install https://github.com/shadowsocks/shadowsocks/archive/master.zip

3.安装vim，执行命令

> yum install vim

4.新建shadowsocks的配置文件，执行命令

> vim ss.json

输入以下内容

```json
{
    "server":"0.0.0.0",
    "server_port":8888,
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"123456",
    "timeout":300,
    "method":"aes-256-cfb"
}
```

5.启动命令

> ssserver -c ss.json -d start

6.防火墙设置

- 关闭防火墙

> systemctl stop firewalld.service

- 禁止防火墙开机自启

> systemctl disable firewalld.service

7.安装bbr加速（貌似centOS 8已经自带了，所以这一步也省了）

- 下载安装脚本

> wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh

- 修改文件的执行权限

> chmod +x bbr.sh

- 启动安装

> ./bbr.sh

按任意键开始安装。安装完成一会之后它会提示我们是否重新启动，我们输入`y`确定重启服务器,或者自己用`reboot`命令手动重启。重启之后，输入`lsmod | grep bbr`，如果看到`tcp_bbr`就说明`bbr`已经启动了。
