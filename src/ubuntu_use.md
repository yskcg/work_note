7. ngix 服务器安装
	1. sudo apt-get install ngix,自动安装成功，共享的目录为:
	``/usr/share/nginx/html``通过http 可以访问该目录
	2. alise 别名访问
	访问同ip下的其他路径，配置例子如下：
	
	配置路径：
	>```/etc/nginx/sites-available```
	>
	配置方法为：
	>
  `location /upgrade {
                try_files $uri $uri/ =404;
                root /home/builder;
        }`

8. 从文件中读取第一行
  `` sed -n 1p file``
