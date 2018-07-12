
# 网页执行shell等脚本


![](https://img.jinchuang.org/github/fcgiwrap-shelllog1.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllog2.png)
![](https://img.jinchuang.org/github/fcgiwrap-shellhome.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllist1.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllist-disk.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllist-ps.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllist-server.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllist-ssh.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllist-uptime.png)
![](https://img.jinchuang.org/github/fcgiwrap-shellmenu.png)

## 说明

- :gem: 基本功能就是把linux命令可以放到网页中去完成
- :gear: 定时刷新数据，时间自定义
- :globe_with_meridians: 本地和远程机器都可以，远程机器数据返回会慢一点
- :triangular_ruler: 页面样式比较low，你可以改为你想要的样式
- :rocket: 参考模板可以添加修改各种你想执行的命令
- :1234: 数据显示样式可以自定义修改
## 安装使用
安装文档: [Nginx支持web界面执行bash.python等脚本](https://me.jinchuang.org/archives/114.html)

NGINX 配置：
```bash
location ~ ^/jcmon/api/ {  #这里的后缀匹配根据需要修改
	gzip off;
	fastcgi_pass  unix:/tmp/fcgiwrap.socket;
	#fastcgi_index index.cgi;
	include fastcgi_params;
	fastcgi_param  SCRIPT_NAME        $document_root$fastcgi_script_name;
}

```

