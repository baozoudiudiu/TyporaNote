## github打不开

1. 通过站长工具找出DNS地址：进入站长工具网站的域名解析网址：[http://tool.chinaz.com/dns/](https://links.jianshu.com/go?to=http%3A%2F%2Ftool.chinaz.com%2Fdns%2F) ，在A类型的查询中输入github.com，找出最快的IP地址

   ![image](https://upload-images.jianshu.io/upload_images/1561402-ad2eaace6497b86a.png)

2. 复制 /etc/host文件到桌面上(在这里不能编辑)，添加对应的IP到里面`52.74.223.119 github`
3. 复制编辑好的host文件到/etc/目录，覆盖原来的host文件，需要验证管理员身份

