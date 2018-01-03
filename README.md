## 这个项目是 **docker** 版本的 **lnmp** 开发环境，可以一键生成，并且支持扩展和版本切换，这么牛逼的项目当然不是我写的，是 **fork** [yeszao](https://github.com/yeszao) 大神的，原版移步[这里](https://github.com/yeszao/dnmp)，[官网在这里](https://www.awaimai.com/2120.html)，我只是稍微改了一点点配置方便自己用的。

## **特点：**

- 目前我提交的这个版本信息为：（docker17.06.2-ce + php7.2 + mysql5.7 + nginx1.13.7 + redis4.0.6）可以直接 **pull** 下来就能跑了，要是想跑其他最新的就按照 [官网](https://www.awaimai.com/2120.html) 一步一步来就行了。

- 支持多版本PHP切换（PHP5.4、PHP5.6、PHP7.2...)

- 支持绑定任意多个域名

- 支持 **HTTPS** 和 **HTTP/2** 具体怎么做原版有说明，我就不啰嗦了

- **PHP** 源代码位于 **host** 中

- **MySQL data** 位于 **host** 中

- 所有配置文件可在 **host** 中直接修改

- 所有日志文件可在 **host** 中直接查看

- 内置完整 **PHP** 扩展安装命令

- 实现一次配置，可在任何支持 **Docker** 系统使用

## 最直接的开始步骤

1. ```shell git clone https://github.com/zhugeliange/dnmp.git ``` 直接克隆源码

2. ```shell docker-compose up``` 启动多个容器

3. 说出来你可能不信已经成功了，不出意外你现在直接访问本地的地址就可以了。

*我自己的服务器已经用这个脚本全面升级了，使用到现在也确实会有一些坑，不过只要你对docker命令熟悉，实际上还是可以解决的，如果还有疑问可以@我或者参考我的这篇* [docker教程](http://fsociety.cn/post/docker%E5%90%A7)

## 注意！注意！注意！

> 下面是一些踩过得坑，估计你们也会遇到，我就写在这里提醒下吧。。。

- 我这里用的是 **unbuntu 16.04lts** 版本，下载安装的是 **docker17.06.2-ce** 这个是个人服务器版，不同的系统版本 **docker** 安装的不一样，这个自己去[官网](https://www.docker.com/)按照文档一步步来就行了。PS：要是英文不好这我也没办法。。。

- 除了 **docker** 之外这里还要装 **docker-compose**，这个是官方出的用来管理多容器的， **linux** 版本的话是分开装的，**windows** 的话桌面版全部是集成安装好了的。

- 万恶的墙，你懂的，默认 **docker** 全部是从官方仓库下载数据的，所以会特别慢，这里用阿里云的镜像加速，自己去阿里云开通一下容器服务就行了，不要钱的。**ubuntu** 的直接敲这个
```shell
sudo mkdir -p /etc/docker
```
```shell
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://wly9i3tz.mirror.aliyuncs.com"]
}
EOF
```
```shell
sudo systemctl daemon-reload
```
```shell
sudo systemctl restart docker
```
其他系统看阿里云的说明就好了。

- 这里面应该挂个代理，在相应版本 **php** 文件夹下的 **Dockerfile** 文件里面找到这个一行 ```shell RUN pear config-set http_proxy http://10.0.75.1:1080``` 把里面的 **ip** 换成刚刚阿里云给你的加速器的地址，注意是 **ip** 地址，并且没有 **http://**。阿里云给你的加速地址默认是域名的形式，你直接八度搜一下 **ip** 地址查询，然后把这个域名解析下就能知道实际的 **ip** 地址了。你要是直接下载我的源码的话我已经配好了，你用我的也行。

- 如果用的是 **php7.2** 版本的话得把根目录下的 **Dockerfile** 文件里面的 
```shell RUN apt-get install -y libmcrypt-dev```
 ```shellRUN docker-php-ext-install mcrypt```
 这两行删掉，我这里的源码已经删了，如果是用的原版的话这里得注意下。

- 另外其他的类似于 **HTTPS**， 还是配置域名站点等官网都有说明我就不啰嗦了。

## 好了废话说完了，完结撒花。再次膜拜 [yeszao](https://github.com/yeszao) 大神。
