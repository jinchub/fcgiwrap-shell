
# 网页执行shell脚本python等脚本

## 说明
:triangular_ruler:
- 基本功能就是把linux命令可以放到网页中去完成
- 页面中点击一次执行一次命令/刷新一次对应网页执行一次命令
- 本地和远程机器都可以，远程机器基于你用命令什么去获取内容
- 参考模板可以添加修改各种你想执行的命令
- 数据显示样式可以自定义修改
- 不支持动态内容和交互式命令

## 安装使用
安装文档: [Nginx支持web界面执行bash.python等脚本](https://me.jinchuang.org/archives/114.html)  
远程机器执行命令，主机可以通过sshpass/export/免密登录/ansible等功能实现

NGINX 转发配置：
```bash
#脚本存放目录自定义 例如放在/jcmon/api/目录
location ~ ^/jcmon/api/ {
	gzip off;
	fastcgi_pass  unix:/tmp/fcgiwrap.socket;
	#fastcgi_index index.cgi;
	include fastcgi_params;
	fastcgi_param  SCRIPT_NAME        $document_root$fastcgi_script_name;
}

```

执行的脚本例子【就是html+脚本的结合，html代码需要用echo " "方式】
```bash
#!/bin/bash
echo "Content-Type:text/html;charset=utf-8"
echo ""

#自动刷新网页,定时去执行查看磁盘使用功能情况
echo "<meta http-equiv="refresh" content="60">"

#html+css样式+命令
echo '<div style="padding-left:10px;">'
ip="这里改为你的机器ip即可"
echo '<h1 style="color:red;border-left:4px solid;padding:4px;">硬盘使用情况</h1>'
echo '<h5 style="color:#848484;">'
dd=`date`
echo "统计时间: $dd [60s刷新一次] 【当前机器ip: $ip】"
echo '</h5>'
echo '<pre style="border-left: 4px solid rgb(12, 40, 245);padding:5px;color:#fff;">'
#本地服务器
df -hT

#远程服务器
#sshpass -p 'passwd' ssh root@$ip -o StrictHostKeyChecking=no 'df -hT'
echo '</pre>'
```
## 效果
![disk](https://me.jinchuang.org/usr/uploads/2020/12/59793653.png)
