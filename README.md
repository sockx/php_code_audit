# 🎉PHP代码审计、动态调试 Docker环境🎉


## F5配置说明
> `port`是`vscode`所在服务器的端口，`phpxdebug`原理是服务器反连开发工具来实现的。

> `pathMappings`中的`/app`是远程目录，他的值是开发工具中`项目文件夹`所对应的路径。
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Listen for Xdebug",
      "type": "php",
      "request": "launch",
      "port": 9003,
      "pathMappings": {
        "/app": "${workspaceRoot}/app/DVWA-2.1"
      }
    }
  ]
}
```

## 不同版本的PHP环境修改
> `/php/phpx.x`中存放不同PHP版本的镜像构建脚本，由于默认拉取镜像是不开启DEBUG信息的，所以需要本地修改。

> `Dockerfile`中`xdebug.client_host`为宿主机，如果是远程镜像，那么需要修改此脚本将`xdebug`工具所在地址填入其中。

> `Dockerfile`中`xdebug.client_port`为端口，需要与`vsode`配置中的`port`保持一直。

```Dockerfile
# Configure xdebug settings
RUN cat >> /usr/local/etc/php/php.ini <<EOF
[xdebug]
# zend_extension=xdebug.so
xdebug.mode=debug
xdebug.start_with_request=yes
xdebug.client_host=host.docker.internal
xdebug.client_port=9003
EOF
```
