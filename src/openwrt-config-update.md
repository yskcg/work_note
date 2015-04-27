###open-wrt 配置升级概要设计文档
####第一章 概述
现在设备不能对服务器对设备的配置及时更新，必须要重新启动路由器才能使配置生效，所以现在需要一种新的机制来解决该问题。
该文档主要来阐述设备更新服务器对设备的配置，具体包括以下的内容：
- **重启**
-  **配置文件更新（认证配置，nginx, portal)**


---
####第二章 方案的总体流程图

设备从本地获取配置版本后，发送请求到server端检测是否是最新的配置，如果是最新的配置，下载该配置并更新配置。
```flow
st=>start: Start
e=>end
cond=>condition: timeout?
op1=>operation: 获取本地配置版本
op2=>operation: 发送版本检查到服务器
cond1=>condition: 最新版本Yes or No?
op3=>operation: 下载配置并更新

st->cond->op1->op2->cond1->op3->cond
cond(yes)->op1
cond(no)->e
cond1(yes)->op3
cond1(no)->e
```
---
#### 第三章 服务器处理
[服务器接口需要补充完善](www.joyotime.com)

---
#### 第四章 路由器处理

---
#####4.1 配置版本号获取
认证配置，nginx, portal，reboot 这4个将被统一看作是一个配置，该配置的版本号初始值与openwrt 版本号相同,如下：
- 文件路径
`/etc/openwrt_release`
- 配置版本号
`DISTRIB_RELEASE="0.0.3"`
`DISTRIB_CONFIG_VERSION="0.0.3"`

- 获取版本号后，将发送**HTTP-header**：
1. 请求类型：**POST**
2.  header字段应当包含且不局限：
**moid**：路由的id号
**version**:*设备当前配置版本号*
**dt**:*设备型号*
**...**
- 服务器收到该请求后，返回的数据应为：
1. 返回值类型：**JSON**；
2. 数据内容应当包含且不局限于该内容：
	` {
	version: "0.x.xxxx", 
	upgrade: "0/1", 
	reboot: "0/1", 
	authed: "0/1",
	ngnix: "0/1",
	portal: "0/1",
	shell: "shell script",//下载完成需要执行的脚本
	files: [
		{
			file: "/path", //保存到设备上的路径和名称
			name: "md5sum", //文件内容md5值，用来验证下载文件正确性
			mode: "777", //文件的权限
			exec: "0/1", //下载完成执行文件
			version: "0.x.xxxx", //文件的版本
			md5: "文件内容的MD5值"
		}...]`

 **这里将所有的配置文件也进行了统一处理，也即是，所有的配置文件将被打包压缩成一个文件来进行下发，对需要更新的配置文件在json中做了字段解析：**
 -  0：不更新该配置文件
 -  1：更新该配置文件

---

#####4.2配置的获取

若如果需要更新配置，设备端将发送HTTP请求到指定的路径下去下载已经打包好的配置文件，发送的**HTTP-header**应当包含且不局限以下字段：

 -  moid：路由的id号
 -  K：加密认证字符串
 -  version：版本号
 -  name：文件名

当获取到新的配置版本后成功加载**authed,ngnix,portal其中之一**或者**reboot 有更新**，`DISTRIB_CONFIG_VERSION`字段将被改写成最新的版本号，该版本号通过服务器下发。

设备获取到的服务器下发的配置文件后，将进行MD5值校验，解压缩，匹配更新标准后，进行配置的加载。

流程如下：

```flow
st=>start: Start
e=>end
cond=>condition: update?
op1=>operation: 下载配置文件
cond1=>condition:  MD5校验合法？
cond2=>condition:  config-update Yes or No?
op3=>operation:   加载配置

st->cond->op1->cond1->cond2->op3->e
cond(yes)->op1
cond(no)->e
cond1(yes)->cond2
cond1(no)->
cond2(yes)->op3
cond2(no)->e
```





