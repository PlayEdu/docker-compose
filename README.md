## PlayEdu docker-compose 构建

### 背景

此项目提供 `docker-compose` 一键运行 `PlayEdu` 。提供一下软件环境：

- PlayEdu v1.4
- MySQL 5.7.42
- Redis 7.0.2
- MinIO - 由 bitnami 封装的 MinIO 发行版本

### 注意

### 快速上手

#### 第一步、克隆本仓库

```
git clone https://github.com/PlayEdu/docker-compose.git playedu-docker-compose
```

#### 第二步、构建镜像

> 下面命令 # 开头的是对下一行命令的注释，无需执行

```
# 进入到 playedu-docker-compose 目录
cd playedu-docker-compose

# 构建镜像
sudo docker-compose build
```

#### 第三步、运行 `MySQL`, `Redis`, `MinIO`

> 1.下面命令是在 playedu-docker-compose 目录执行  

```
# #### 这里是注释的话，无需执行 ####
# 命令解释：复制 .env.example 并命名为 .env
cp .env.example .env

# #### 这里是注释的话，无需执行 ####
# .env.example 是我们预置的默认的运行环境变量，比如：运行的端口号、数据库名等
# 如果您对这一快不很熟悉的话，建议您无需修改 .env 文件内容，因为修改了内容
# 按照本文下面的流程可能就无法走通

# #### 这里是注释的话，无需执行 ####
# 命令解释：给 data 授权可读、可写、可执行权限
# data 目录将会挂载到容器以用来数据化持久存储(更多知识请自行了解 docker 数据卷)
chmod a+rwx data

# #### 这里是注释的话，无需执行 ####
# 命令解释：运行容器
sudo docker-compose up -d mysql redis minio
```

执行上述命令会很快返回结果，但是这并不意味着上述三个软件就已经成功的运行了。它们的初始化运行都需要一段过程，这里我们稍微等待 1-2 分钟的时间（机器配置高的话可能时间更短）。

#### 第四步、运行 `PlayEdu`

> 下面命令是在 playedu-docker-compose 目录执行

```
sudo docker-compose up -d playedu
```

执行完成之后，等待 15s 左右的时间就可以访问了。

#### 第五步、系统配置 - `MinIO` 配置

浏览器打开 `http://你的服务器IP:9900` ，在登录窗口输入账号 `admin@playedu.xyz` 和密码 `playedu` 进入到后台，然后打开系统配置，选择 `MinIO` 配置，请填入下表的内容并保存：

| 配置项      | 需要配置的值               |
| ----------- | -------------------------- |
| `AccessKey` | `username`                 |
| `SecretKey` | `password`                 |
| `Bucket`    | `playedu`                  |
| `Endpoint`  | `http://你的服务器IP:9002` |
| `Domain`    | `http://你的服务器IP:9002` |

### 链接

| 平台           | 地址                        | 默认账号            | 密码       |
| -------------- | --------------------------- | ------------------- | ---------- |
| API 服务       | `http://你的服务器IP:9700`  | -                   | -          |
| PC 学员端口    | `http://你的服务器IP:9800`  | -                   | -          |
| H5 学员端口    | `http://你的服务器IP:9801`  | -                   | -          |
| 后台管理端口   | `http://你的服务器IP:9900`  | `admin@playedu.xyz` | `playedu`  |
| MinIO 管理端口 | `http://你的服务器IP:50002` | `username`          | `password` |
