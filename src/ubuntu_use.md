#**ubuntu FAQ：**

1. 升级过程中断电，导致不能正常开机进入 advance Ubuntu 选择比较老的linux kernel 头启动，后进行全新的升级，可能会出现，readline 之类，删除，添加密匙，某些软件卸载不成功，全部备份后删除即可。

2. 分辨率设置-arandr
>安装这个软件，进行图形化设置，并适配。

3. 升级后，System seting 里面东西没有了
>运行 sudo apt-get install unity-control-center，重新安装解决
4. 设定root 密码
 >Sudo passwd root

5. mount 网络挂载没有写权限
	1. id xxx(用户名)
		uid=1000(ysk) gid=1000(ysk) groups=1000(ysk)
		要mount 的机器的用户名
	2. mount
```sudo mount -o rw,uid=1000,gid=1000,username=yangshaokun,password=yang5775847  //192.168.2.140/yangshaokun/work /home/ysk/work ```

6. ubuntu 图形界面卡死解决
>1.  Ctrl + Alt + F1 转到tty1或者 用ssh 连接上Ubuntu也可以
>2.  ps -t -tty7 查看进程
>3.  找到Xorg进程到PID号 xxx
>4.  kill xxx

7. ngix 服务器安装
	1. sudo apt-get install ngix,自动安装成功，共享的目录为:
	>```/usr/share/nginx/html```
	通过http 可以访问该目录
	2. alise 别名访问
	访问同ip下的其他路径，配置例子如下：
>	配置路径：
	>```/etc/nginx/sites-available```
>	配置方法为：
	>```location /upgrade {
                try_files $uri $uri/ =404;
                root /home/builder;
        }```

8. 从文件中读取第一行
  >``` sed -n 1p file```
