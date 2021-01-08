# fee 灯塔项目运行环境安装及配置

>官方教程是使用 docker (比较耗费内存和性能) 集成环境,本教程使用适用于 linux 的 Windows(Windows10) 子系统 WSL 2 分发安装 ubuntu

## 1.下载安装 WSL 2
[安装WSL 2 官方教程](https://docs.microsoft.com/zh-cn/windows/wsl/about)
<br>
<br>教程很详情,跟着提示步骤一步一个脚印的来即可,墙裂推荐直接安装 WSL 2版本

### "点击安装WSL" 按钮 ==> 选择并点击 "手动安装" ==> 按照 "手动安装步骤" 操作下一步.

注意事项: 
 * 建议严格按照教程步骤进行安装配置,防止出现奇怪问题.
 <br>
 * 步骤6 打开  Microsoft Store 商店时,如果出现类似于下方等打不开的情况,检查是否启用了代理,关闭所有代理,然后重新打开商店.

![](https://github.com/HUYIJUNCODING/firefly/blob/main/doc/assets/1.png)
<!-- ![](http://static.ledouya.com/Ft-SFeRe0EbP4J3uZPTioNx_iDy-) -->

* 分发版本较多,选择自己感兴趣的即可,也可以同时安装多个分发,但是感觉没太大必要,若选择 ubuntu 建议安装 Ubuntu 18.04 LTS 版本,本教程就是基于此版本,出了问题,网上此版本下的解决方案很多.
* 最后一步的 "为新的 Linux 分发版创建用户帐户和密码"的密码很重要,之后 bash 窗口使用管理员权限运行命令时都要校验密码,因此不要忘记喽.


## 2. 下载安装 node.js
* 推荐使用 Node.js 版本管理工具,好处是可以下载管理多个 Node.js 版本,需要使用那个版本切那个即可,目前比较主流的管理工具有两个,nvm 和 n,关于 nvm 和 n 的区别可以自行百度,我习惯使用 nvm,看个人风格喜好,其实功能差不多.

* 可参考资料<br>
	[nvm](https://github.com/nvm-sh/nvm)<br>
	[如何在 Ubuntu 上安装 Node.js 和 npm](https://developer.aliyun.com/article/760687)<br>
	[Ubuntu下安装node.js](https://cloud.tencent.com/developer/article/1508330)

### 2.1 更新工具包
```
sudo apt-get update
```


### 2.2 安装服务器维护日常依赖,执行命令

 ```
 sudo apt-get install vim openssl build-essential libssh-dev wget curl
 ```

### 2.3 安装 nvm
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
或者
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```


**注意: 这里的命令执行时候可能会报错,我安装的时候使用第一个会报错,第二个命令可执行安装,因此都试下,一个不行换另一个即可.**

### 2.4 验证 nvm 是否安装成功
```
nvm -v 或者 nvm ls
```
**注意: 如果报 nvm 找不到,则关闭 bash 重新打开,如果依然还报命令找不到,则说明缺少环境变量,去配置下即可**
```js
  1. cd ～/.nvm
  
  2. ls 命令查看查看目录下文件列表,若无 .bash_profile文 件，则创建该文件并编辑
  	touch .bash_profile
	vim .bash_profile
    
  3. 编辑内容直接粘贴
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```
### 2.5 安装 Node.js 和 npm

```
nvm list-remote (查看nvm 远程可安装的 node 版本)
nvm install node (安装最新可用的版本)
nvm install --lts (安装最新的长期稳定版)
nvm install 14.15.0 (安装指定版本,这里以安装 14.15.0 这个版本为示例)
nvm ls (查看当前已安装的 node 版本)
nvm use 14.15.0 (切换到指定node版本,这里以 14.15.0 这个版本为示例)
```
## 3. 下载安装 mysql
[ubuntu 18.04 安装 mysql-server](https://wangxin1248.github.io/linux/2018/07/ubuntu18.04-install-mysqlserver.html)<br>
<br>
ubuntu 18.04 安装 mysql 参考这篇文章就够了,很详细,按照步骤一步一步来即可.<br>

**注意事项**
* 运行安全脚本：`$ sudo mysql_secure_installation` 时候如果报错,则关闭当前 bash 窗口重新打开,然后输入命令,成功后继续按照教程提示下一步即可.
<br>
* 若遇到报 `ER_NOT_SUPPORTED_AUTH_MODE`,则请参考这篇文章来解决.<br>[解决Node.js mysql客户端不支持认证协议引发的“ER_NOT_SUPPORTED_AUTH_MODE”问题](https://waylau.com/node.js-mysql-client-does-not-support-authentication-protocol/)
<br>
* 设置root用户的密码的时候不要忘记喽,之后登录数据库需要验证,此密码可以被重置,但是尽量还是不要忘记.
<br>
* 若执行 `mysql -u root -p` 报  `Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)` 则先执行 `sudo service mysql start` 启动服务,然后执行  `mysql -u root -p`命令连接服务.
<br>
* 若执行 `mysql -u root -p` 报 `ERROR 1698 (28000): Access denied for user 'root'@'localhost'` 则命令前加 sudo 运行,即`sudo mysql -u root -p` .

## 4. 下载安装 redis
[ubuntu 18.04 安装 Redis](https://www.cnblogs.com/ycx95/p/11725458.html)<br>
<br>
ubuntu 18.04 安装 Redis 参考这篇文章就够了,很详细,按照步骤一步一步来即可.

**注意事项**<br>
* 参考教程中启动/关闭/重启 redis 命令用的是 `sudo systemctl start redis`, `sudo systemctl stop redis`, `sudo systemctl restart redis`, 如果不生效, 则改用 `sudo service redis-server start`, `sudo service redis-server stop`, `sudo service redis-server restart` 命令.
<br>
* 运行命令 `service --status-all` 来查看服务名称(启动/关闭/重启服务时候不确定服务名称的话可以查看).

![](https://github.com/HUYIJUNCODING/firefly/blob/main/doc/assets/2.png)
<!--![](http://static.ledouya.com/FlfgBuioJCUTlioMgvoIixe92znm)  -->



可参考资料:<br>
	[How To Install and Secure Redis on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-redis-on-ubuntu-18-04)<br>
    [System has not been booted with systemd as init system (PID 1). Can't operate](https://stackoverflow.com/questions/52197246/system-has-not-been-booted-with-systemd-as-init-system-pid-1-cant-operate)

## 5. vscode 安装插件 Remote - WSL
* 该插件可以实现在 windows 系统上基于已安装的 WSL 环境运行 linux 程序的能力,终端输入 linux 命令,跟 ubuntu bash 窗口作用一样.很方便,墙裂推荐安装使用.

## 6. 克隆并配置项目,安装依赖,启动项目
* client 客户端是前端 vue 项目,npm i 安装依赖 (如果下载慢,可以设置 npm 源来加速,或者安装 cnpm 加速),然后 npm run dev 运行项目,linux 环境下启动即可(因为 linux 环境下也装了 node.js ,所以可以运行前端项目)
* server 服务端安装依赖的时候不出意外的话会在安装 `node-rdkafka` 和 `sqlite3` 的时候报错,下面是解决步骤.
### 6.1 从 gitHub 上 clone 项目到本地
```
git clone git@github.com:LianjiaTech/fee.git
```
[仓库地址](https://github.com/LianjiaTech/fee)

### 6.2 vscode 导入项目(使用 Remote WSL 插件 )
* 点击 vscode 右下角图标(如图所示)
![](https://github.com/HUYIJUNCODING/firefly/blob/main/doc/assets/3.png)
<!--![](http://static.ledouya.com/FsTSqqDi8ncH5H-6ZIYiFvFfVvT8)  -->

* 弹出下拉框中选择 "Open Folder in WSL..." 去选择想导入的项目
* 导入成功后标识如图
![](https://github.com/HUYIJUNCODING/firefly/blob/main/doc/assets/4.png)
<!--![](http://static.ledouya.com/FkI4wYBsyunr0ESZ0XcZCUFsPnO8)  -->

### 6.3 配置MySQL
* 在 `server/src/configs/mysql.js` 中修改主机地址/数据库端口/数据库用户名/数据库密码/数据库库名
```
const development = {
  host: '127.0.0.1', // 主机地址
  port: '3306', // 数据库端口
  user: 'root', // 数据库用户名
  password: '00000000', // 数据库密码
  database: 'platform'  // 数据库库名
}
```
### 6.4 配置redis
* 在server/src/configs/redis.js中修改主机地址或redis端口
```
// 开发环境配置
const development = {
  host: '127.0.0.1', // 主机地址
  port: '6379' // redis端口
}
```

### 6.5 安装服务端依赖，在项目 server 目录下

```
npm install
```

#### 6.5.1 针对 node-rdkafka,sqlite3 依赖包报错解决方案

* 1. 在 ubuntu 上安装 GCC
[如何在ubuntu 18.04上安装GCC编译器](https://www.myfreax.com/how-to-install-gcc-compiler-on-ubuntu-18-04/)<br>
参考文档一步步安装 GCC编译器 即可.第一步安装 gcc 的原因是 node-rdkafka 的需要用到 node-gyp,而 node-gyp 的安装又依赖 gcc.

* 2. 在 ubuntu 上 安装 python2.7 版本
 安装  python2.7 的原因是 sqlite3 需要用到 node-pre-gyp ,而 node-pre-gyp 的安装又依赖 python2.7.

```
sudo add-apt-repository ppa:fkrull/deadsnakes

sudo apt-get update

sudo apt-get install python2.7

//切换 python 版本,ubuntu18.04 默认 安装 的是 python3.6, 因此安装 python2.7 后需要切换到当前版本才可以使用,有点类似 nvm 切换 node 版本.
//sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 10  中最后一个参数指定了此选项的优先级,数值越大,优先级越高,会被指定为当前默认python版本,这里10就表示优先级等级

sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 10 

或者

sudo update-alternatives --config python


其他命令:
python --version (查看当前使用的 python 版本)
update-alternatives --list python  (列出当前已安装且可用的所有 python 版本)
```

### 6.6 编译 server，打开一个新的窗口在项目 server 目录下(vscode终端或者 ubuntu bash都可以,一定要 cd 到项目 server 目录下)
```
npm run watch
```
### 6.7 启动server服务，在项目 server 目录下(vscode终端或者 ubuntu bash都可以,一定要 cd 到项目 server 目录下)

```
npm run dev
```
### 6.8 创建数据库

* 在项目 server 目录下执行下方指令，会在当前目录下生成 init.sql 文件

```
npm run fee Utils:GenerateSQL 1 '2020-01' '2020-07' > init.sql
```
* 创建 platform 数据库
```
<!-- CREATE DATABASE 数据库名; -->
create database platform;

<!-- 创建完成后可执行 SHOW DATABASES; 命令查看创建结果 -->
```
**注意** 如果没有启动服务,必须先启动 mysql服务,然后登录 mysql 服务,才可以开始创建数据库以及使用 sql 命令

* 在项目 server 目录下执行下列指令,读取 init.sql 文件,为 platform 数据库建表
```
mysql -u root -h 127.0.0.1 platform -p < init.sql
```
**注意** 需要注释/删除掉 int.sql 文件开头两行,否则会执行报错(sql文件中,非sql语句不能执行)

```
<!-- 这两行非sql语句注释掉 -->
> platform@1.0.0 fee /mnt/c/custom/youran/repositories/fee/server
> NODE_ENV=development node dist/fee.js "Utils:GenerateSQL" "1" "2020-01" "2020-07"
```

### 6.9 初始化样例数据。在项目 server 目录下，执行下列指令
```
npm run fee Utils:TemplateSQL
```
执行成功后，样例数据会被写入数据库中。

### 6.10 安装 Client 依赖，在项目 client 目录下
```
npm install
```
### 6.11 启动 Client 服务，在项目 client 目录下
```
nmp run dev
```
### 6.12 访问本地服务: 127.0.0.1:8080

* a. 使用默认管理员账户登录
   账号：test@qq.com
   密码：admin

* b. 或进行注册、登录，就能看到模板项目数据了。

可参考资料:
[Error installing node-gyp on ubuntu](https://stackoverflow.com/questions/21155922/error-installing-node-gyp-on-ubuntu)<br>
[npm install 报错:node-pre-gyp ERR! 问题解决](https://www.cnblogs.com/haochuang/p/5688093.html)<br>
[Ubuntu18.04下python版本完美切换的解决方法](https://www.geek-share.com/detail/2771497709.html)<br>







