
# 网页执行shell脚本python等脚本

## 功能说明
- 基本功能就是把linux命令可以放到网页中去完成
- 页面中链接点击一次执行一次命令|刷新一次命令链接的网页执行一次命令
- 本地和远程机器都可以，远程机器基于你用命令什么去获取内容
- 脚本模板可以修改各种你想执行的命令
- 页面数据显示样式可以自定义修改
- 不支持动态内容和交互式命令

## 安装使用
安装文档: [Nginx支持web界面执行bash.python等脚本](https://me.jinchuang.org/archives/114.html)  
远程机器执行命令，主机可以通过sshpass/export/免密登录/ansible等功能实现


启动 fcgiwrap服务：
```bash
/etc/init.d/fcgiwrap start
```

NGINX 转发配置：
```bash
#执行的脚本目录自定义，例如放在/linux-command/page/script/目录(linux-command为根目录)
location ~ ^/linux-command/page/script/ {
	gzip off;
	fastcgi_pass  unix:/tmp/fcgiwrap.socket;
	#fastcgi_index index.cgi;
	include fastcgi_params;
	fastcgi_param  SCRIPT_NAME        $document_root$fastcgi_script_name;
}

```

执行的脚本例子【就是html+linux脚本的结合，html代码需要用echo ''方式】
#!/bin/bash
echo "Content-Type:text/html;charset=utf-8"
echo "" 

# 自动刷新当前页面
#echo "<script>window.setInterval(function(){
#	window.location.reload();
#},1000);</script>"
#echo "<meta http-equiv="refresh" content="60">"

# css样式
echo '<style>
body{color:#cecece;}
.title{color: #FF9800;border-left: 4px solid;padding: 4px;}
pre{font-size:14px;border-left: 4px solid #4CAF50;padding: 5px;}
</style>'

# 定义变量
ip="192.168.16.188"
dd=`date`

echo '<div style="padding-left:10px;">'

# 标题
echo '<h1 class="title">硬盘使用情况</h1>'

# 内容
echo '<h5 style="color:#848484;">'
echo "统计时间: $dd 【当前机器ip: $ip】"
echo '</h5>'

# 命令返回结果
echo '<pre>'
# 本机获取磁盘使用
df -hT
# 远程机器获取磁盘使用(使用sshpass)
sshpass -p "password" ssh root@$ip -o StrictHostKeyChecking=no  'df -hT'
echo '</pre>'

echo '</div>'
```
## 效果
![disk](https://me.jinchuang.org/usr/uploads/2020/12/59793653.png)
