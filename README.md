
# 网页执行shell等脚本


![](https://img.jinchuang.org/github/fcgiwrap-shelllog.png)
![](https://img.jinchuang.org/github/fcgiwrap-shellhome.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllist1.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllist-disk.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllist-ps.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllist-server.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllist-ssh.png)
![](https://img.jinchuang.org/github/fcgiwrap-shelllist-uptime.png)
![](https://img.jinchuang.org/github/fcgiwrap-shellmenu-1.png)

## 说明

- :gem: 基本功能就是把linux命令 可以放到网页中去完成
- :triangular_ruler: 样式比较low，你可以改为你想要的样式

## 使用

```bash
location ~ ^/jcmon/api/ {  #这里的后缀匹配根据需要修改
	gzip off;
	fastcgi_pass  unix:/tmp/fcgiwrap.socket;
	#fastcgi_index index.cgi;
	include fastcgi_params;
	fastcgi_param  SCRIPT_NAME        $document_root$fastcgi_script_name;
}

```

