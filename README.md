Docker Nginx Map Port and Dir Demo
==================================

使用docker nginx来为本机的文件提供网站服务.

```
docker run --name my-nginx -v /some/content:/usr/share/nginx/html:ro -p 8080:80 -d nginx
```

其中:

- `--name my-nginx`：给这个container指定名字为`my-nginx`，方便查看
- `-v /some/content:/usr/share/nginx/html:ro`: 把本机的`/some/content`映射到docker container中的`/usr/share/nginx/html`目录（就是nginx需要的），`ro`表示readonly
- `-p 8080:80`：表示把本机的`8080`端口映射到container中的`80`，这样我们访问本机`80`端口即可
- `-d`: detach，表示在后台执行，将会打印出container id
- `nginx`: 表示要执行的image名字为`nginx`，由于没有指明版本，所以会取`nginx:latest`

使用local-site目录
--------------

我们已经准备好了`local-site`目录，下面我们将把它映射给nginx container。

由于`-v`参数中只能使用绝对路径，所以我们需要通过拿到`./local-site`的绝对路径：

Fish下是：

```
(pwd)/local-site
```

Bash下是：

```
`pwd`/local-site
```

在Fish下：

```
docker run --name my-nginx -v (pwd)/local-site:/usr/share/nginx/html:ro -p 8080:80 -d nginx
```

如果是在Ubuntu下，打开<http://localhost:8080>就能看到页面上写着`Hello, Nginx in Docker`

如果是Mac，需要使用`docker-machine ip`命令拿到当前docker machine的ip后访问：

![demo](./images/demo.jpg)