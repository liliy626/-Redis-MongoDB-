# -Redis-MongoDB-

# 部署说明书

## 1. 项目概述

### 1.1 项目名称
- **项目名称**：商品信息智能管控平台：Redis+MongoDB集成方案

### 1.2 项目描述
- **描述**：该系统用于管理商品信息，包括商品的添加、删除、修改和查询功能。系统使用 MongoDB 作为数据库，Redis 作为缓存，Spring Boot 作为后端框架。 
主要分为四个模块:

- **用户管理模块** 
：用户登录、注册、密码找回（通过邮箱方式）、用户信息修改、密码修改

- **仪表盘管理模块**
：展示当前月收入及其环比环比=（当前月收入 - 上个月收入）/ 上个月收入）、当前月订单数及其环比、网站访问量、当前月退单数及其环比、以条形图的形式(使用jquery插件）展示最近30天每天的收入和订单数

- **商品管理模块**
：商品增删改查、商品图片导入（存储在MongoDB）、导出商品报表、商品分类增删改查、库存查改，库存不足和积货提醒、商品回收和恢复。

- **订单管理模块**
：订单查询查看、订单退款管理（查看和审批）、发货管理、物流公司管理、快递跟踪（调用快递100接口）

### 主要用到的技术：
- 使用maven进行项目构建 
- 使用Springboot+Mybatis搭建整个系统 
- 使用Thymeleaf模板技术实现页面静态化
- 使用框架Bootstrap、JQuery开发前端界面  
- 使用MySQL和MongoDB分别存储数据和图片
- 使用Redis缓存来提升数据库查询性能


## 2. 环境要求

### 2.1 硬件要求
- **CPU**：至少 2 核
- **内存**：至少 4 GB
- **存储**：至少 20 GB 可用空间

### 2.2 软件要求
- **操作系统**：windows、linux 或 macOS
- **浏览器**：Chrome、Firefox 或 Safari
- **Java**：JDK 11 或更高版本
- **MongoDB**：版本 4.0 或更高版本
- **Redis**：版本 5.0 或更高版本
- **Maven**：版本 3.6 或更高版本（用于构建项目）

## 3. 部署步骤

### 3.1 安装 Java

```bash
sudo apt update
sudo apt install openjdk-11-jdk
```

### 3.2 安装 MongoDB

```bash
# 导入 MongoDB 公共 GPG 密钥
wget -qO - https://www.mongodb.org/static/pgp/server-4.0.asc | sudo apt-key add -

# 创建 MongoDB 源列表文件
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/multiverse amd64/packages/ mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list

# 更新包列表并安装 MongoDB
sudo apt update
sudo apt install -y mongodb-org
```

### 3.3 启动 MongoDB

```bash
sudo systemctl start mongod
sudo systemctl enable mongod
```

### 3.4 安装 Redis

```bash
sudo apt update
sudo apt install redis-server
```

### 3.5 启动 Redis

```bash
sudo systemctl start redis-server
sudo systemctl enable redis-server
```

### 3.6 部署应用程序

#### 3.6.1 克隆项目

```bash
下载项目到本地
```

#### 3.6.2 构建项目

```bash
mvn clean install
```

#### 3.6.3 运行应用程序

1. 将sql文件在MySQL运行生成表和数据，启动Redis服务， MongoDB选择性开启（不开启时会报错但不影响系统正常访问，用到上传照片功能需要启动MongoDB）
2. 最后直接启动Application类后访问[http://localhost:8080/user/login]就可以进入本系统！

## 4. 配置文件

### 4.1 MongoDB 配置

在 `application.properties` 文件中配置 MongoDB 连接：

```properties
spring.data.mongodb.uri=mongodb://localhost:27017/jesper
```

### 4.2 Redis 配置

在 `application.properties` 文件中配置 Redis 连接：

```properties
spring.redis.host=localhost
spring.redis.port=6379
```

## 5. 访问应用程序

- **访问地址**：`http://localhost:8080`
- **默认管理员账户**：
  - 用户名：`admin`
  - 密码：`admin`

## 6. 常见问题

### 6.1 MongoDB 连接失败

- 确保 MongoDB 服务正在运行。
- 检查 `application.properties` 中的 MongoDB URI 是否正确。

### 6.2 Redis 连接失败

- 确保 Redis 服务正在运行。
- 检查 `application.properties` 中的 Redis 配置是否正确。

## 7. 维护和更新

- 定期备份 MongoDB 数据库。
- 更新依赖库和服务器软件以保持安全性。

---
