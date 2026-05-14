# Hermes Web UI 安装指南

## 这是什么
Hermes Agent 的 Web 聊天界面，支持多会话 / 定时任务管理 / 文件管理 / 技能管理。

## 前置要求
- Node.js >= 23.0.0
- Windows 系统（当前环境是 Win11）

## 第一步：检查 Node.js 版本
```powershell
node --version
# 必须是 v23.x 或更高。如果不是，去 https://nodejs.org 下载最新版
```

## 第二步：安装（二选一）

### 方式 A：npm 全局安装（推荐，最简单）
```powershell
npm install -g hermes-web-ui@0.5.17
```
> ⚠️ 注意！包名是 `hermes-web-ui`，不要拼错。版本指定 `@0.5.17` 确保装的是正确的版本。
> 网上搜到的 v0.13 是另一个不相关的项目，不要用。

### 方式 B：从 GitHub 克隆（可修改源码）
```powershell
git clone https://github.com/EKKOLearnAI/hermes-web-ui.git
cd hermes-web-ui
npm install
npm run build
npm install -g .   # 注册到全局
```

## 第三步：配置连接 Hermes API Server

创建配置文件 `%USERPROFILE%\.hermes-web-ui\config.yaml`：

```yaml
# 连接本地 Hermes API Server
api:
  baseUrl: "http://localhost:8642"
  token: "你的 Hermes API Token"

# 默认模型
model:
  default: "deepseek-v4-flash"
```

> 💡 API Token 在你启动 Hermes Agent 的终端日志里能找到，格式类似 `API key: sk-xxx`。

## 第四步：启动 Web UI

```powershell
hermes-web-ui
```

默认地址：**http://localhost:8648**

## 第五步：验证是否启动成功
打开浏览器访问 http://localhost:8648
- 看到登录/会话界面 ✅
- 能选择模型聊天 ✅
- 侧边栏有：会话管理 / 定时任务 / 文件管理 / 技能管理 ✅

如果看到的是空白或完全不同的界面 → 说明装错了版本，卸载后重试：
```powershell
npm uninstall -g hermes-web-ui
npm cache clean --force
# 然后重新按第二步安装
```

## 常见问题

| 问题 | 解决 |
|------|------|
| 端口被占用 | 修改 config.yaml 加 `port: 8649` |
| Token 不知道在哪 | 打开 Hermes CLI 终端，看启动日志里 `API key: sk-...` |
| 装成了 v0.13 | 说明包名搞混了。`npm uninstall -g 错误包名`，重装 `hermes-web-ui@0.5.17` |
| 连不上 API | 检查 Hermes API Server 是否在运行（默认为端口 8642） |
