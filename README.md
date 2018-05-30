# cassso
使用cas框架来实现统一登录(单点登录)功能
cas服务器安装步骤：
1，在本地配置多个域名。如：www.cobee.com.cn, news.cobee.com.cn, blog.cobee.com.cn
2，生成安全访问证书：
    a, 用java工具keytool生成用户身份证书
    keytool -genkey -alias cobee -keyalg RSA -keystore d:/caskey/cobeekey(不创建文件夹, cobeekey是一个文件)
    密钥库口令：123456    cobee密钥口令：666666
    b, 导出证书
    keytool -export -file d:/caskey/cobee.crt -alias cobee -keystore d:/caskey/cobeekey
    c, 导入证书到jvm安装目录里面的jre目录里(-keystore目录不能有空格)
    keytool -import -keystore D:\Program Files\Java\jre1.8.0_144\lib\security\cacerts -file d:/caskey/cobee.crt -alias cobee
    