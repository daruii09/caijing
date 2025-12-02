# API配置说明

## 📝 配置文件位置

API配置文件位于：`config/api.js`

## 🔧 配置方法

### 1. 修改API地址

打开 `config/api.js` 文件，修改对应环境的 `baseURL`：

```javascript
const config = {
	development: {
		baseURL: 'http://localhost:8080/api',  // 开发环境API地址
		timeout: 10000,
	},
	production: {
		baseURL: 'https://api.yourdomain.com/api',  // ⚠️ 请修改为真实的生产环境API地址
		timeout: 15000,
	},
	test: {
		baseURL: 'https://test-api.yourdomain.com/api',  // ⚠️ 请修改为测试环境API地址
		timeout: 10000,
	}
}
```

### 2. 环境变量配置

项目会根据 `process.env.NODE_ENV` 自动选择对应的配置：
- `development` - 开发环境
- `production` - 生产环境
- `test` - 测试环境

### 3. 使用环境变量（推荐）

如果需要使用环境变量，可以创建 `.env` 文件：

```bash
# .env.development
VITE_API_BASE_URL=http://localhost:8080/api

# .env.production
VITE_API_BASE_URL=https://api.yourdomain.com/api
```

然后在 `config/api.js` 中使用：

```javascript
const config = {
	development: {
		baseURL: import.meta.env.VITE_API_BASE_URL || 'http://localhost:8080/api',
		timeout: 10000,
	},
	// ...
}
```

## 📋 API接口列表

所有API接口定义在 `api/index.js` 文件中：

### 登录相关 (`loginApi`)
- `login(data)` - 用户登录
- `register(data)` - 用户注册
- `sendCode(data)` - 发送验证码
- `resetPassword(data)` - 重置密码
- `logout()` - 退出登录
- `getUserInfo()` - 获取用户信息

### 资产相关 (`assetsApi`)
- `getAssetsOverview()` - 获取资产总览
- `getAssetsList(params)` - 获取资产列表
- `getAssetsDetail(id)` - 获取资产详情
- `getTransactionList(params)` - 获取交易记录
- `getHistoryIncome(params)` - 获取历史收益
- `getPublicAssetsDetail(id)` - 公募资产详情
- `getPrivateAssetsDetail(id)` - 私募资产详情
- `getWalletAssetsDetail(id)` - 钱包资产详情
- `sellAssets(data)` - 卖出资产
- `appointmentAssets(data)` - 资产预约

### 产品相关 (`productApi`)
- `getProductList(params)` - 获取产品列表
- `getProductDetail(id)` - 获取产品详情
- `getProductHistoryNet(id, params)` - 获取产品历史净值
- `purchase(data)` - 购买产品
- `getNewFundList(params)` - 获取新基金列表
- `getPrivateFundList(params)` - 获取私募基金列表
- `getOptionalFundList(params)` - 获取自选基金列表
- `addOptional(productId)` - 添加自选
- `removeOptional(productId)` - 取消自选

### 服务相关 (`serviceApi`)
- `openAccount(data)` - 开户
- `riskAssessment(data)` - 风险评估
- `getRiskAssessmentResult()` - 获取风险评估结果
- `addBankCard(data)` - 添加银行卡
- `getBankCardList()` - 获取银行卡列表
- `deleteBankCard(id)` - 删除银行卡
- `uploadPhoto(filePath, type)` - 上传照片

### 消息相关 (`messageApi`)
- `getMessageList(params)` - 获取消息列表
- `getMessageDetail(id)` - 获取消息详情
- `markAsRead(id)` - 标记消息已读
- `getUnreadCount()` - 获取未读消息数
- `getPlatformNotice(params)` - 获取平台公告
- `submitFeedback(data)` - 提交建议反馈

### 账户相关 (`accountApi`)
- `changeLoginPassword(data)` - 修改登录密码
- `changeTradePassword(data)` - 修改交易密码
- `changePhone(data)` - 修改手机号
- `getAccountInfo()` - 获取账户信息
- `recharge(data)` - 充值
- `withdraw(data)` - 提现
- `getTransactionRecords(params)` - 获取交易记录

## 🔐 请求拦截器

所有请求会自动添加以下处理：

1. **Token自动添加**：如果存在token，会自动添加到请求头 `Authorization: Bearer {token}`
2. **统一错误处理**：401错误会自动跳转登录页
3. **加载提示**：默认显示加载提示（可通过 `loading: false` 关闭）

## 📝 使用示例

```javascript
import { loginApi } from '@/api/index'

// 登录
try {
	const res = await loginApi.login({
		username: '13800138000',
		password: '123456'
	})
	console.log('登录成功', res.data)
} catch (error) {
	console.error('登录失败', error)
}

// 获取产品列表（不显示加载提示）
const res = await productApi.getProductList({
	page: 1,
	pageSize: 20
}, {
	loading: false
})
```

## ⚠️ 注意事项

1. **生产环境部署前**：务必修改 `production` 环境的 `baseURL` 为真实的API地址
2. **HTTPS**：生产环境建议使用HTTPS协议
3. **跨域问题**：开发环境如果遇到跨域问题，需要在后端配置CORS或使用代理
4. **Token管理**：Token会自动保存到本地存储，退出登录时会清除

## 🔄 更新日志

- 2024-01-01: 初始版本，包含所有基础API接口

