# FitReserve - 健身房管理系统

基于 Spring Boot + Vue 的健身房管理系统，涵盖会员管理、课程预约、商品购买、余额充值等核心业务功能。

## 项目简介

本系统是一个完整的健身房管理平台，采用前后端分离架构，支持管理员和会员两种角色。系统提供会员办卡/续卡、健身课程管理及报名、健身商品管理及购买、余额充值、到期提醒等功能，满足健身房日常运营管理需求。

## 功能模块

| 模块 | 说明 |
| --- | --- |
| 会员管理 | 会员信息注册、查询、修改、删除 |
| 会员办卡 | 会员办理健身卡，选择卡类型及有效期 |
| 会员续卡 | 会员到期后续卡，延长有效期 |
| 会员类型 | 管理不同会员卡类型（有效天数、售价、详情） |
| 教练管理 | 教练信息维护（姓名、年龄、教龄等） |
| 健身课程 | 课程发布与管理（分类、时间、课时、费用） |
| 报名课程 | 会员在线报名课程 |
| 健身商品 | 商品上架与管理（分类、规格、价格、库存） |
| 购买商品 | 会员在线购买健身商品 |
| 余额充值 | 会员账户余额充值 |
| 到期提醒 | 会员卡到期自动提醒 |
| 收藏功能 | 会员收藏课程或商品 |
| 公告管理 | 系统公告/新闻发布 |
| 关于我们 | 机构介绍信息管理 |
| 系统简介 | 系统基本信息展示 |

## 技术栈

### 后端

- **框架**: Spring Boot 2.2.2
- **ORM**: MyBatis Plus 2.3
- **权限**: Apache Shiro 1.3.2
- **数据库**: MySQL
- **其他**: FastJSON、Hutool、Baidu AI SDK、Apache POI

### 前端

- **框架**: Vue 2.6
- **UI 组件**: Element UI 2.13
- **图表**: ECharts 5.4
- **路由**: Vue Router 3.1
- **HTTP**: Axios
- **富文本**: vue-quill-editor
- **地图**: vue-amap
- **其他**: js-md5、print-js、vue-json-excel

## 项目结构

```
fitreserve/
├── src/main/java/com/
│   ├── controller/          # 控制层 - 处理 HTTP 请求
│   ├── dao/                 # 数据访问层 - MyBatis Mapper 接口
│   ├── entity/              # 实体层
│   │   ├── model/           # 请求参数模型
│   │   ├── view/            # 视图模型（关联查询）
│   │   └── vo/              # 值对象（响应封装）
│   ├── service/             # 业务逻辑层
│   │   └── impl/            # 业务实现
│   └── utils/               # 工具类
├── src/main/resources/
│   ├── application.yml      # 应用配置
│   ├── mapper/              # MyBatis XML 映射文件
│   └── admin/admin/         # 前端项目（Vue）
│       ├── src/             # 前端源码
│       ├── public/          # 静态资源
│       └── package.json     # 前端依赖配置
├── picture/                 # 项目截图
├── pom.xml                  # Maven 依赖配置
└── README.md
```

## 环境要求

- **JDK**: 1.8+
- **Node.js**: 12.x+
- **MySQL**: 5.7+
- **Maven**: 3.6+

## 快速开始

### 1. 数据库配置

创建 MySQL 数据库，数据库名为 `gym4`：

```sql
CREATE DATABASE gym4 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

数据库连接配置位于 [application.yml](src/main/resources/application.yml)，默认配置：

```yaml
spring:
  datasource:
    url: jdbc:mysql://127.0.0.1:3306/gym4?useUnicode=true&characterEncoding=utf-8&serverTimezone=GMT%2B8
    username: root
    password: root
```

请根据实际环境修改用户名和密码。

### 2. 后端启动

```bash
# 安装依赖并启动
mvn spring-boot:run
```

后端服务启动在 `http://localhost:8080/gym`。

### 3. 前端启动

```bash
cd src/main/resources/admin/admin

# 安装依赖
npm install

# 启动开发服务器
npm run serve
```

### 4. 构建部署

```bash
# 后端打包
mvn clean package -DskipTests

# 前端构建
cd src/main/resources/admin/admin
npm run build
```

## 配置说明

| 配置项 | 默认值 | 说明 |
| --- | --- | --- |
| 服务端口 | 8080 | `server.port` |
| 上下文路径 | /gym | `server.servlet.context-path` |
| 文件上传限制 | 300MB | `spring.servlet.multipart.max-file-size` |
| 主键策略 | 用户输入ID | MyBatis Plus `id-type: 1` |

## 许可证

本项目仅供学习参考使用。