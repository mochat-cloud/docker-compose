# 环境准备
## 一、前置
依赖
* docker，docker-compose
* wget -c https://github.com/mochat-cloud/mochat.git
* wget -c https://github.com/mochat-cloud/docker-compose.git

```
注意：
1、mac版docker.desktop版本推荐3.0以上，以避免内存飙高问题
2、我们假定两个项目为同级目录，如下
mochat-cloud/mochat 下载目录为 /path/to/mochat；
mochat-cloud/docker-compose 下载目录为 /path/to/docker-compose；

```

## 二、配置
### 2.1 docker-compose 配置
- `cd /path/to/docker-compose`
- `cp .env.example .env`，根据自己的项目，修改相应配置
- `cp docker-compose.sample.yml docker-compose.yml`

- 2.2 vhost配置，推荐使用 [SwitchHosts](https://github.com/oldj/SwitchHosts/blob/master/README_cn.md)

```
127.0.0.1 api.mochat.com
127.0.0.1 scrm.mochat.com
127.0.0.1 sidebar.mochat.com
127.0.0.1 op.mochat.com
```

提示：
```
1、api.mo.chat为占用域名，请避免使用
2、.dev与.app域名为chrome域名，使用chrome时请避免使用
3、使用非本地容器MySQL时，可以设置MYSQL_CONNECT_TYPE=cloud，并修改CLOUD_MYSQL_*相应属性即可
```

## 三、运行
```
cd /path/to/docker-compose
docker-compose build
docker-compose up
```
提示：
- docker-compose up执行时，dashboard、sidebar、operation、mochat_init容器运行完后会自动退出显示

```
dashboard exited with code 0
sidebar exited with code 0
operation exited with code 0
mochat_init exited with code 0
```
这属于正常现象，不属于error

- 运行成功
运行时间根据不同主机配置、网络速度不同，可能会时间过长，请耐心等待
```
stone@localhost docker-compose % docker-compose ps            
   Name                  Command               State                     Ports                  
------------------------------------------------------------------------------------------------
backend       /bin/sh -c sh -c "composer ...   Up       0.0.0.0:9501->9501/tcp                  
dashboard     /bin/sh -c sh -c "yarn ins ...   Exit 0        
operation     /bin/sh -c sh -c "yarn ins ...   Exit 0                                           
mochat_init   /bin/sh -c sh -c "/tmp/wai ...   Exit 0                                           
mysql         docker-entrypoint.sh mysqld      Up       0.0.0.0:3306->3306/tcp, 33060/tcp       
nginx         /docker-entrypoint.sh ngin ...   Up       0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
redis         docker-entrypoint.sh redis ...   Up       0.0.0.0:6379->6379/tcp                  
sidebar       /bin/sh -c sh -c "yarn ins ...   Exit 0
```

- 如果初始化失败，可重新初始化
```
cd /path/to/docker-compose
rm ./services/mochat_init/install.lock
docker-compose up mochat_init
```

### 3.1 如果热更新
- 后端PHP热更新，可以 `./servers/php/Dockerfile` 内改 `php /opt/www/bin/hyperf.php start` 为 `php /opt/www/bin/hyperf.php server:watch`
- 前端热更新建议在宿主机 `npm run dev`，接口调试地址为 `http://api.mochat.com`

### 3.2 登陆
- 在浏览器输入 http://scrm.mochat.com
- 默认的用户名密码: `18888888888` / `123456`
- 进入项目，在`系统设置` -> `授权管理` 中点击 `添加企业微信号`
- 如果您没有企业微信号，您可以到企业微信官网网站注册调试用的`企业微信号`