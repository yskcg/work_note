##bash note##
1. 提取fram num
>//use awk and sed grep 提取RX 接收口的fram 包个数,例子
>ifconfig eth0 | grep "RX packets:"| awk  '{print $2}' | sed 's/^packets://g' >/tmp/eth0-2_pa

2. 提取ip addr
>ifconfig eth0 | grep "inet addr:"| awk  '{print $2}' | sed 's/^addr://g' >/tmp/eth0-2_pa

3:字符串转化函数编写

4. bash 比较大小
	**整数比较**
>>`
	-eq                等于,如:if [ "$a" -eq "$b" ]
	-ne                不等于,如:if [ "$a" -ne "$b" ]
	-gt                大于,如:if [ "$a" -gt "$b" ]
	-ge                大于等于,如:if [ "$a" -ge "$b" ]
	-lt                小于,如:if [ "$a" -lt "$b" ]
	-le                小于等于,如:if [ "$a" -le "$b" ]
	<                小于(需要双括号),如"$a" < "$b")
	<=                小于等于(需要双括号),如"$a" <= "$b")
	>                大于(需要双括号),如"$a" > "$b")
	>=                大于等于(需要双括号),如"$a" >= "$b")

	字符串比较
	=                等于,如:if [ "$a" = "$b" ]
	==                等于,如:if [ "$a" == "$b" ],与=等价
					注意:==的功能在[[]]和[]中的行为是不同的,如下:
					1 [[ $a == z* ]]    # 如果$a以"z"开头(模式匹配)那么将为true
					2 [[ $a == "z*" ]]  # 如果$a等于z*(字符匹配),那么结果为true
					3
					4 [ $a == z* ]      # File globbing 和word splitting将会发生
					5 [ "$a" == "z*" ]  # 如果$a等于z*(字符匹配),那么结果为true
					一点解释,关于File globbing是一种关于文件的速记法,比如"*.c"就是,再如~也是.
					但是file globbing并不是严格的正则表达式,虽然绝大多数情况下结构比较像.
	!=                不等于,如:if [ "$a" != "$b" ]
					这个操作符将在[[]]结构中使用模式匹配.
	<                小于,在ASCII字母顺序下.如:
					if [[ "$a" < "$b" ]]
					if [ "$a" \< "$b" ]
					注意:在[]结构中"<"需要被转义.
	>                大于,在ASCII字母顺序下.如:
					if [[ "$a" > "$b" ]]
					if [ "$a" \> "$b" ]
					注意:在[]结构中">"需要被转义.
					具体参考Example 26-11来查看这个操作符应用的例子.
	-z                字符串为"null".就是长度为0.
	-n                字符串不为"null"
					注意:
					使用-n在[]结构中测试必须要用""把变量引起来.使用一个未被""的字符串来使用! -z
					或者就是未用""引用的字符串本身,放到[]结构中(见Example 7-6)虽然一般情况下可
					以工作,但这是不安全的.习惯于使用""来测试字符串是一种好习惯.[1]
`					
5. 需要在ubus 下注册接口函数
	>`ls /var/run/ubus.sock`
	使用例子如下：
>`
	ubus call iwinfo info '{ "device": "wlan0"}'
	ubus call iwinfo devices
	ubus list iwinfo -v
`	
6. bash 字符串截取
	命令的2种替换形式 $()和 ``
	示例：截断字符串    
	a):
		#截取文件名称
		`var1=$(basename /home/aimybbe/bash/test.sh)
		echo $var1
		`
		#截取目录
		`var2=$(dirname /home/aimybbe/bash/test.sh)
		echo $var2
		`
	b):
		`var1=`basename /home/aimybbe/bash/test.sh`
		echo $var1
		
		var2=$(dirname /home/aimybbe/bash/test.sh)
		echo $var2
	
	${varible##*string} 从左向右截取最后一个string后的字符串
	${varible#*string}从左向右截取第一个string后的字符串
	${varible%%string*}从右向左截取最后一个string后的字符串
	${varible%string*}从右向左截取第一个string后的字符串
	“*”只是一个通配符可以不要
	`
7. bash 语句第一行含义
	#! 表示用哪个程序来解释该文件的内容，一般写在第一行
8. bash 变量赋值两边不能加空格
	`http://bbs.chinaunix.net/forum.php?mod=viewthread&tid=218853&page=4#pid1511745`
9. 判断文件夹存在
	`if [ -d "xx/yy"]`
10. bash 中的传入参数的参数传入
	`$*为"1 2 3"（一起被引号包住）
	$@为"1" "2" "3"（分别被包住）
	$#为3(参数数量)
`
