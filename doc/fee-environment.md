# fee 灯塔项目运行环境安装配置

>官方教程是使用 docker(很耗费内存和性能) 集成环境,本教程使用适用于 linux 的 Windows(Windows10) 子系统 WSL 2(分发安装 ubuntu)

## 1.下载安装 WSL 2
[安装WSL 2 官方教程](https://docs.microsoft.com/zh-cn/windows/wsl/about)
教程很详情,跟着提示步骤一步一个脚印的来即可,墙裂推荐直接安装 WSL 2版本

### "点击安装WSL" 按钮 ==> 选择并点击 "手动安装" ==> 按照 "手动安装步骤" 操作下一步

注意事项: 
 * 建议严格按照教程步骤进行安装配置,防止出现奇怪问题.
 * 步骤6 打开  Microsoft Store 商店时,如果出现类似于下方等打不开的情况,检查是否启用了代理,关闭所有代理,然后重新打开商店.

![](http://static.ledouya.com/Ft-SFeRe0EbP4J3uZPTioNx_iDy-)

* 分发版本较多,选择自己感兴趣的即可,也可以同时安装多个分发,但是感觉没太大必要,若选择 ubuntu 建议安装 Ubuntu 18.04 LTS 版本,本教程就是基于此版本,出了问题,网上此版本下的解决方案很多.
* 最后一步的 "为新的 Linux 分发版创建用户帐户和密码"的密码很重要,之后 bash 窗口使用管理员权限运行命令时都要校验密码,因此不要忘记喽.


## 2. 下载安装 node.js
* 推荐使用 Node.js 版本管理工具,好处是可以下载管理多个 Node.js 版本,需要使用那个版本切那个即可,目前比较主流的管理工具有两个,nvm 和 n,关于 nvm 和 n 的区别可以自行百度,我习惯使用 nvm,看个人风格喜好,其实功能差不多.

* 可参考资料
[nvm](https://github.com/nvm-sh/nvm)
[如何在 Ubuntu 上安装 Node.js 和 npm](https://developer.aliyun.com/article/760687)
[Ubuntu下安装node.js](https://cloud.tencent.com/developer/article/1508330)

### 更新工具包

 **sudo apt-get update**

### 安装服务器维护日常依赖,执行命令

 *`sudo apt-get install vim openssl build-essential libssh-dev wget curl`*

### 安装nvm

**curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash**
或者
**wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash**


注意: 这里的命令安装时候可能会报错,我安装的时候使用第一个会报错,第二个命令可执行安装,因此都试下,一个不行换另一个即可.

### 验证 nvm 是否安装成功

 **nvm -v** 或者 **nvm ls**


