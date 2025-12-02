# Wealth Uni-App 项目

财富管理 uni-app 应用

## 项目结构

```
wealth/
├── pages/              # 页面目录
│   ├── login/         # 登录相关页面
│   ├── home/          # 首页相关页面
│   ├── assets/        # 资产相关页面
│   ├── product/       # 产品相关页面
│   ├── service/       # 服务相关页面
│   └── kefu/          # 客服页面
├── static/            # 静态资源
│   ├── image/         # 图片资源
│   ├── icon_img/      # 图标资源
│   ├── fonts/         # 字体文件
│   └── js/            # JavaScript文件
├── uni_modules/        # uni-app插件
├── App.vue            # 应用入口
├── main.js            # 主入口文件
├── manifest.json      # 应用配置
├── pages.json         # 页面配置
└── package.json       # 项目配置
```

## 安装依赖

```bash
npm install
```

## 运行项目

### H5
```bash
npm run dev:h5
```

### 微信小程序
```bash
npm run dev:mp-weixin
```

### App
```bash
npm run dev:app
```

## 构建项目

### H5
```bash
npm run build:h5
```

### 微信小程序
```bash
npm run build:mp-weixin
```

### App
```bash
npm run build:app
```

## 主要功能模块

- **登录注册**: 用户登录、注册、密码重置
- **首页**: 轮播图、快捷菜单、推荐产品
- **资产**: 总资产展示、公募/私募/钱包管理
- **产品**: 基金产品列表、产品详情、购买
- **服务**: 开户服务、风险评估、银行卡管理
- **客服**: 在线客服功能

## 技术栈

- Vue 3
- uni-app
- uni-ui

## 注意事项

1. 请确保已安装 HBuilderX 或使用 CLI 方式开发
2. 静态资源路径请使用相对路径或绝对路径
3. 生产环境请移除 console 语句
4. API 接口地址请在配置文件中统一管理

