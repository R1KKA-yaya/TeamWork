# TeamWork - 校园论坛系统

## 📝 项目简介

TeamWork 是一个基于 Nuxt.js (前端) 和 Java Spring Boot (后端) 构建的现代化校园论坛系统。项目旨在为在校学生提供一个便捷的在线交流、信息共享和互助平台。用户可以浏览帖子、发表自己的见解、参与讨论、分享文件等。系统同时配备了后台管理功能，方便管理员对用户、内容及系统进行维护。

## ✨ 主要功能

### 前台功能 (用户端)
*   **用户认证**:
    *   用户注册与登录 (`pages/register.vue`, `pages/userlogin.vue`, `api/login.js`)
    *   密码重置 (`pages/User/profile/resetPwd.vue`)
*   **个人中心**:
    *   用户信息展示与修改 (`pages/User/profile/userInfo.vue`, `api/userInfo.js`)
    *   头像更换 (`pages/User/profile/userAvatar.vue`)
    *   邮箱绑定/修改 (`pages/User/profile/userEmail.vue`)
*   **内容互动**:
    *   帖子浏览 (首页 `pages/index.vue`, 内容展示 `components/Content.vue`)
    *   帖子发布 (`pages/User/publish.vue`)，支持文件上传 (`components/ContentFile.vue`)
    *   帖子评论与回复 (`components/Comment.vue`, `components/CommentChild.vue`)
    *   帖子点赞 (相关逻辑，数据库有 `Like` 表)
    *   按分类查看帖子 (数据库有 `Category` 表)
*   **校园特色**:
    *   校园侧边栏/特定板块 (`components/CampusSide.vue`, `utils/campus.js`)

### 后台管理功能 (管理员端 - `campus-admin` 模块)
*   **系统监控**: 监控系统运行状态 (`campus-admin/.../monitor`)
*   **系统管理**:
    *   用户管理
    *   内容管理 (帖子、评论等)
    *   分类管理
    *   权限管理 (推测)

## 🛠️ 技术栈

### 前端
*   **核心框架**: Nuxt.js (基于 Vue.js)
*   **UI 组件**: 自定义组件 (`components/`), 可能包含自定义UI样式 (`assets/style/wooui.css`)
*   **状态管理**: Vuex (`store/`)
*   **路由**: Nuxt.js 自动生成路由 (`pages/`)
*   **API 请求**: 基于 `utils/request.js` 的封装 (通常为 Axios)
*   **样式**: SCSS (`assets/style/campus.scss`), CSS
*   **工具库**: `utils/` 下包含认证、表单验证、错误处理等辅助函数

### 后端 (基于 Java)
*   **核心框架**: Spring Boot (根据模块化结构和常见 Java 项目实践推测，如 `campus-framework`, `campus-common`)
*   **模块化设计**:
    *   `campus-common`: 公共模块，包含通用工具类、常量、枚举、异常处理、自定义注解等。
    *   `campus-framework`: 框架核心模块，提供安全 (`security`)、切面 (`aspectj`)、配置 (`config`)、数据访问 (`mapper`) 等支持。
    *   `campus-admin`: 后台管理模块，提供系统监控和管理相关的 Controller。
    *   `campus-modular`: 业务功能模块，包含核心业务逻辑 (`core`)、API 接口 (`api`)、Controller (`controller`)、Service (`service`)、Mapper (`mapper`) 等。
*   **数据校验**: `campus-common/validator`
*   **任务处理**: `campus-modular/src/main/java/com/campus/business/task` (可能包含定时任务等)
*   **(推测)** `ruoyi.js` 的存在可能表明后端部分功能或设计思想借鉴了若依 (RuoYi) 框架。

### 数据库
*   关系型数据库 (如 MySQL, PostgreSQL 等，具体未指明)。
    *   通过 `campus-common/utils/sql` 和 `campus-framework/mapper` 进行数据操作。

## 📂 项目结构

### 前端项目结构 (Nuxt.js)

```plaintext
.
├── .nuxt/              # Nuxt.js 构建和临时文件目录
├── api/                # 后端接口调用封装
│   ├── login.js
│   └── userInfo.js
├── assets/             # 静态资源 (会被 Webpack 处理)
│   ├── icons/
│   │   └── svg/        # SVG 图标
│   ├── images/         # 图片资源
│   └── style/          # 样式文件 (SCSS, CSS)
├── components/         # 全局 Vue.js 组件
│   ├── CampusSide.vue
│   ├── Comment.vue
│   └── ...
├── layouts/            # 布局组件
│   ├── default.vue
│   ├── myfooter.vue
│   └── myheader.vue
├── pages/              # 页面组件 (Nuxt.js 基于此生成路由)
│   ├── index.vue
│   ├── register.vue
│   ├── userlogin.vue
│   └── User/
│       ├── management.vue
│       ├── publish.vue
│       └── profile/
│           └── ...
├── static/             # 纯静态资源 (直接拷贝到项目根目录)
│   └── favicon.ico
├── store/              # Vuex 状态管理
│   └── README.md
└── utils/              # 工具函数和辅助模块
    ├── auth.js
    ├── request.js
    └── ...
```

### 后端项目结构 (Java - 多模块)

```plaintext
.
├── campus-admin/               # 校园论坛系统的后台管理模块
│   └── src/main/java/com/campus/admin/
│       ├── config/
│       └── controller/
│           ├── monitor/
│           └── system/
├── campus-common/              # 校园论坛系统的公共模块
│   └── src/main/java/com/campus/common/
│       ├── annotation/
│       ├── config/
│       ├── constant/
│       ├── domain/             # 实体类
│       ├── enums/              # 枚举类
│       ├── exception/          # 异常处理
│       ├── filter/
│       └── utils/              # 工具类 (http, ip, sql, uuid)
│       └── validator/          # 数据校验
├── campus-framework/           # 校园论坛系统的框架模块
│   └── src/main/java/com/campus/framework/
│       ├── api/
│       ├── aspectj/            # AOP
│       ├── config/
│       ├── expander/
│       ├── handler/
│       ├── interceptor/        # 拦截器
│       ├── listener/
│       ├── manager/
│       ├── mapper/             # MyBatis Mapper 接口 (推测)
│       └── security/           # 安全控制 (如 Spring Security)
└── campus-modular/             # 校园论坛系统的功能模块
    └── src/main/java/com/campus/
        ├── business/           # 核心业务模块
        │   ├── api/
        │   ├── controller/
        │   ├── core/
        │   ├── domain/
        │   ├── enums/
        │   ├── mapper/
        │   ├── service/
        │   ├── system/
        │   └── task/
        └── web/                # (可能与Web特定配置或组件有关)
```

## 🗄️ 数据库设计 (主要表结构)

以下是本系统核心数据表的设计概览：

**用户表 (User)**
| 字段名    | 类型    | 描述               |
| ---------- | ------- | ------------------ |
| id         | int     | 用户ID，主键       |
| username   | varchar | 用户名             |
| password   | varchar | 密码 (通常加密存储) |
| email      | varchar | 邮箱               |
| created_at | datetime| 注册时间           |

**管理员表 (Admin)**
| 字段名    | 类型    | 描述               |
| ---------- | ------- | ------------------ |
| id         | int     | 管理员ID，主键     |
| username   | varchar | 用户名             |
| password   | varchar | 密码 (通常加密存储) |

**帖子表 (Content)**
| 字段名      | 类型    | 描述               |
| ----------- | ------- | ------------------ |
| id          | int     | 帖子ID，主键       |
| title       | varchar | 标题               |
| content     | text    | 内容               |
| user_id     | int     | 发帖用户ID (外键, 关联 User.id) |
| category_id | int     | 分类ID (外键, 关联 Category.id) |
| created_at  | datetime| 发帖时间           |

**分类表 (Category)**
| 字段名    | 类型    | 描述               |
| ---------- | ------- | ------------------ |
| id         | int     | 分类ID，主键       |
| name       | varchar | 分类名称           |

**评论表 (Comment)**
| 字段名    | 类型    | 描述               |
| ---------- | ------- | ------------------ |
| id         | int     | 评论ID，主键       |
| content    | text    | 评论内容           |
| user_id    | int     | 评论用户ID (外键, 关联 User.id) |
| content_id | int     | 帖子ID (外键, 关联 Content.id) |
| created_at | datetime| 评论时间           |

**点赞表 (Like)**
| 字段名    | 类型    | 描述               |
| ---------- | ------- | ------------------ |
| id         | int     | 点赞ID，主键       |
| user_id    | int     | 点赞用户ID (外键, 关联 User.id) |
| content_id | int     | 帖子ID (外键, 关联 Content.id) |

**文件表 (File)**
| 字段名    | 类型    | 描述               |
| ---------- | ------- | ------------------ |
| id         | int     | 文件ID，主键       |
| filename   | varchar | 文件名             |
| url        | varchar | 文件存储路径/URL   |
| content_id | int     | 帖子ID (外键, 关联 Content.id, 可选，若文件与帖子关联) |


## 🚀 如何开始

### 环境准备
*   **前端**: Node.js (建议 LTS 版本), npm 或 yarn
*   **后端**: JDK (如 Java 8, 11, 17), Maven 或 Gradle, 数据库 (如 MySQL)
*   **开发工具**: VS Code (前端), IntelliJ IDEA (后端)

### 安装与运行 (示例)

**前端:**
```bash
# 进入前端项目目录 (假设名为 frontend)
cd <frontend_project_directory>

# 安装依赖
npm install
# 或者
yarn install

# 启动开发服务器 (通常访问 http://localhost:3000)
npm run dev
# 或者
yarn dev
```

**后端:**
1.  配置数据库连接信息 (通常在 `application.properties` 或 `application.yml` 文件中)。
2.  初始化数据库表结构 (可能需要手动执行 SQL 脚本或依赖 JPA/MyBatis 自动生成)。
3.  使用 Maven/Gradle 构建项目并运行 Spring Boot 应用。
    ```bash
    # 进入后端项目根目录 (包含各模块的父目录)
    cd <backend_project_directory>

    # 使用 Maven (示例)
    mvn spring-boot:run -pl campus-modular # (假设 campus-modular 是主启动模块)
    # 或者在 IDE 中直接运行主应用类
    ```

> **注意**: 请根据项目的实际构建配置和启动方式调整上述命令。

## 🤝 贡献指南

欢迎对本项目进行贡献！如果您有任何改进建议或发现任何问题，请通过以下方式参与：
1.  Fork 本仓库
2.  创建您的特性分支 (`git checkout -b feature/AmazingFeature`)
3.  提交您的更改 (`git commit -m 'Add some AmazingFeature'`)
4.  将更改推送到分支 (`git push origin feature/AmazingFeature`)
5.  开启一个 Pull Request

## 📄 许可证

[ 根据您的项目选择合适的开源许可证，例如：MIT License ]

---

希望这份 README 对您有所帮助！
