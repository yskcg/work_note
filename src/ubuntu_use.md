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
	``/usr/share/nginx/html``通过http 可以访问该目录
	2. alise 别名访问
	访问同ip下的其他路径，配置例子如下：
	
	配置路径：``/etc/nginx/sites-available``
	
	配置方法为：
	>
  `location /upgrade {
                try_files $uri $uri/ =404;
                root /home/builder;
        }`

8. 从文件中读取第一行
 > ` sed -n 1p file`
9. 添加个人用户到samba 贡献
>
>1. 在配置文件`/etc/samba/smb.conf`添加如下内容：
`[xxx]
  comment = samba user
  browseable = yes
  path = /home/yangshaokun
  guest ok = no
  public = no
  writable = yes `
>2. 在用户控制文件`/etc/samba/smbuser`添加上用户名：
 >`xxx=xxx`

10. kermit send 调用的是lrzsz 软件包中的lsz ，lsz 需要建立到sz的软链接
>> ```sudo apt-get install lrzsz```

11. git 添加多个密钥
>> ```ssh-keygen -t rsa -f ~/.ssh/自己命名的文件 -C "email"```

12.ubuntu install java
>>
`sudo cp /home/yourname/Doenloads/jdk-7u21-linux-i586.tar.gz /opt
cd /opt 
sudo tar -zxvf jdk-7u21-linux-i586.tar.gz . (解压到/opt目录)```
>>　设置环境变量
>>>　　在/etc/profile中添加JDK配置信息：
sudo gedit /etc/profile
在最后添加如下内容：# set jdk environment
export JAVA_HOME=/opt/jdk1.7.0_21
export JRE_HOME=/opt/jdk1.7.0_21/jre
export CLASSPATH=.:$CLASSPATH:$JAVA_HOME/lib:$JRE_HOME/lib
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin`

source /etc/profile （让刚刚的配置生效）
