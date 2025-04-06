# micro-apps-root

## 主应用：基座（main-vue3）

> 功能：拿到 token 然后派发到各个子应用

- 登录 /api/auth/login POST
- 登出 /api/auth/logout POST

> 接口说明：

- 登录：传入账号和密码，返回 token。
- 登出：清除 token。

```json
// POST /api/auth/login
{
  "username": "test",
  "password": "123456"
}
// 返回
{
  "token": "mocked-token-123"
}

```

### 子应用：首页（child-nuxt2-home）

> 功能：

- 首页列表 /api/home/list GET

mock 示例：

```json
// GET /api/home/list
[
  { "id": 1, "title": "首页内容一" },
  { "id": 2, "title": "首页内容二" }
]
```

### 子应用：找工作（child-vue2-job）

> 功能：

- 职位列表 /api/job/list GET
- 职位详情 /api/job/detail/:id GET

mock 示例

```json
// GET /api/job/list
[
  { "id": 101, "title": "前端开发", "company": "阿里巴巴" },
  { "id": 102, "title": "后端开发", "company": "腾讯" }
]

// GET /api/job/detail/101
{
  "id": 101,
  "title": "前端开发",
  "description": "负责前端页面开发",
  "company": "阿里巴巴"
}

```

### 子应用：找企业（child-vue3-job）

> 功能：

- 企业列表 /api/company/list GET
- 企业详情 /api/company/detail/:id GET

mock 示例：

```json
// GET /api/company/list
[
  { "id": 201, "name": "字节跳动", "industry": "互联网" },
  { "id": 202, "name": "百度", "industry": "AI" }
]

// GET /api/company/detail/201
{
  "id": 201,
  "name": "字节跳动",
  "industry": "互联网",
  "location": "北京"
}

```

### 子应用：关于我们（child-react18-about）

> 功能：

- 关于我们 /api/about/info GET

mock 示例：

```json
// GET /api/about/info
{
  "company": "微前端平台",
  "description": "一个多技术栈集成的企业级系统"
}
```

1. Mock Server 工具推荐：

- 使用 Mock Service Worker (MSW)（适用于 Vue/React/Nuxt 等）
- 或者本地 node server + json-server/mockjs

2. 接口统一管理：

- 每个子应用维护自己的接口配置
- 主应用统一配置公共接口（如认证相关）

3. 前后端联调方式：

- 使用 axios 拦截器统一处理 token
- 子应用通过环境变量控制是否启用 mock

## 推荐结构

```arduino
micro-apps-root/        ← 顶层 Git 仓库
│
├── micro-main-vue3/          ← 主应用（子模块，独立仓库） git submodule add git@github.com:WNZhao/micro-main-vue3.git
├── micro-child-nuxt3-home/     ← 子模块目录（指向另一个 Git 仓库）git submodule add git@github.com:WNZhao/micro-child-nuxt3-home.git micro-child-nuxt3-home
├── child-vue2-job/     ← 子应用：找工作和找企业（共用或拆分）
├── child-react18-about/← 子应用：关于我们（子模块）
└── README.md

```

> 一次性获取所有 submodule 的最新代码

```bash
# 进入主项目目录
cd main-project

# 初始化并更新所有子模块（如果已存在可以跳过 init）
git submodule update --init --recursive

# 进入每个子模块并切换到主分支（如 main 或 master）并拉取最新
git submodule foreach 'git checkout main || git checkout master; git pull'

```

### micro-main-vue3

```bash
pnpm create vue@latest
# ts
# pina
# vue-router

```
