# cassso
使用cas框架来实现统一登录(单点登录)功能 <br>
cas服务器安装步骤：<br>
1，在本地配置多个域名。如：www.cobee.com.cn, news.cobee.com.cn, blog.cobee.com.cn <br>
2，生成安全访问证书： <br>
    a, 用java工具keytool生成用户身份证书 <br>
    keytool -genkey -alias cobee -keyalg RSA -keystore d:/caskey/cobeekey(不创建文件夹, cobeekey是一个文件) <br>
    密钥库口令：123456    cobee密钥口令：666666 <br>
    b, 导出证书 <br>
    keytool -export -file d:/caskey/cobee.crt -alias cobee -keystore d:/caskey/cobeekey <br>
    c, 导入证书到jvm安装目录里面的jre目录里(-keystore目录不能有空格) <br>
    keytool -import -keystore D:\Java\jre1.8.0_171\lib\security\cacerts -file d:/caskey/cobee.crt -alias cobee <br>
    jre cacerts的密钥库密码：changeit<br>
    d, 删除证书<br>
    keytool -delete -alias cobee -keystore D:\Java\jre1.8.0_171\lib\security\cacerts<br>
3, 把开Tomcat8.0的SSL功能 （/conf/server.xml）<br>
    增加参数说明(注意大小写)：keystoreFile：在第一步创建的key存放位置, keystorePass：创建证书时的密码 <br>
    &lt;Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
           maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
           clientAuth="false" sslProtocol="TLS" keystoreFile="d:/caskey/cobeekey" keystorePass="123456" /&gt; <br>

4, 用https://localhost:8443访问服务器 <br>
5, 用域名访问服务器 （/conf/server.xml）<br>
    &lt;Host name="www.cobee.com.cn"  appBase="webapps"
                unpackWARs="true" autoDeploy="true"&gt;
6, 部署cas应用 <br>
    在maven repository中搜索cas-server-webapp，使用4.2.7版本，下载war文件 <br>
    
7, 访问：https://www.cobee.com.cn:8443/cas/login <br>
    输入默认用户名和密码casuser：Mellon