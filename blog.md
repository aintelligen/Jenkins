# Jenkins

Jenkins 自动化部署

## 准备工作 配置 SSH

[生成 SSH](https://help.aliyun.com/document_detail/51798.html?spm=5176.2020520101.205.d51798.5fa64df5HxA9Tr)  
创建 SSH  
绑定 SSH  
重启服务器

测试 putty SSH 链接服务器

## Jenkins 配置

```shell
#启动 jenkins
java -jar jenkins-war --httpPort=8866
#添加 Publish SSH 插件

#新建项目 源码管理
#构建环境
#Send files or execute commands over SSH before the build starts  删除文件
cd /alidata/blog/
sudo rm -rf /alidata/blog/*

#Provide Node & npm bin/ folder to PATH

#Send files or execute commands over SSH after the build starts  解压文件
cd /alidata/blog/
unzip ./build.zip

# # ssh.ppk  服务器密钥 start pscp.exe  -i  密钥  文件  root@服务器IP:文件位置
start pscp.exe -i D:\Software\Jenkins\SSH\ssh.ppk  C:\Users\CS068MPC\.jenkins\workspace\aintelligen\build.7z root@127.0.0.1:/alidata/blog/

#构建
#Execute Windows batch command 构建项目
npm -v && npm install && npm run build && npm run zip
#Execute Windows batch command 上传文件到服务器
# # ssh.ppk  服务器密钥 start pscp.exe  -i  密钥  文件  root@服务器IP:文件位置
start pscp.exe -i D:\Software\Jenkins\SSH\ssh.ppk  C:\Users\CS068MPC\.jenkins\workspace\aintelligen\build.7z root@127.0.0.1:/alidata/blog/

pscp -i D:\Software\Jenkins\SSH\jenkinsSSH.ppk  D:\github\blog\build.zip  root@127.0.0.1:/alidata/

#安装最新版node
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs


```

[blog](https://aintelligen.com)
