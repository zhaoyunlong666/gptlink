# 常见问题

## 微信系列
### 微信扫码登录提示 AppID 参数错误

需要前往管理后台配置上网站应用的 `APPID` 与 `SECRET` ，网站应用申请 [点击前往](https://open.weixin.qq.com/)

网页授权域名校验文件放置容器内 `/app/gptweb` 目录下即可完成验证。

### 微信登陆提示 redirect_uri 与后台配置不一致

需要前往[微信公众平台](https://mp.weixin.qq.com/)配置网页回调域名为你的域名。

公众号菜单路径：设置与开发 -> 公众号设置 -> 功能设置 -> 网页授权域名

网页授权域名校验文件放置容器内 `/app/gptweb` 目录下即可完成验证。

### 微信扫码提示 Scope参数错误或没有Scope权限

检查是否将公众号 AppId 与 Secret 配置在微信网站应用配置项中。微信网站应用 应前往开放平台申请。

### 微信支付成功但订单显示未支付

检查环境变量 `APP_URL` 是否正确，如不匹配微信回调通知将无法成功，通常配置为 协议 + 域名 + /api/，以下为示例

```txt
示例配置

APP_URL=https://abc.com/api/
...
```

### 任务分享成功，无法获得次数

请检查微信公众号的 IP 白名单是否正确，分享依赖微信 Jssdk 配置，如未配置微信相关服务，建议关闭此任务。


## 运维相关

### Docker 部署时提示服务器错误

1. 检查数据库与 Redis 配置地址是否可正常访问
2. 确保 Mysql 版本大于5.7
3. 可以通过命令 `docker logs gptlink` 查看容器运行是否产生异常。

PS : 不要填写 `127.0.0.1` 或 `localhost`，此地址是指向容器内，容器内并不包含 `Mysql` 和 `Redis` 服务，可以填写本机的内网 IP 如 `192.168.1.100` 或 容器的网关 IP

### Docker-compose 首次运行提示服务器错误

`gptlink` 容器启动时，需要确保 `mysql` `redis` 等服务已启动完成，可通过 `docker-compose logs gptlink`命令查看运行时是否产生异常

### 如何查看服务日志

docker-compose 方式启动的项目，可以在 `docker-compose/data/logs` 目录中查看异常日志。如为 `Docker`方式运行，
可查看 `/app/gptserver/runtime/logs` 目录中的日志内容，或将此目录与宿主机共享


## 其他
### 用户登录方式切换后原账号无法使用
暂不支持 用户名/密码 与 微信登录方式并存

### 如何配置使用 OpenAI 提供的接口

详见ENV部分说明

### 项目中未见包含前端源码

前端开源已经在路上了，还需要一些时间才可发布。
