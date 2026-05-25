# 01 - 在 VS Code 上配置 Claude Code（无需注册）

## 📝 学习目标
了解如何在 VS Code 中配置 Claude Code，无需注册即可使用，并禁用登录提示。

## 🔧 配置步骤

### 1. 安装 Claude Code 插件
首先确保您已经安装了 Claude Code：
```bash
npm install -g @anthropic-ai/claude-code
```

### 2. 配置 settings.json
在 VS Code 中打开用户设置（`Ctrl + ,`），找到或创建 `settings.json` 文件，添加以下配置：

```json
{
    "claudeCode.disableLoginPrompt": true,
    "claudeCode.apiProvider": "deepseek",
    "claudeCode.apiKey": "your-deepseek-api-key",
    "claudeCode.model": "deepseek-chat"
}
```

### 3. 禁用登录提示
设置 `"claudeCode.disableLoginPrompt": true` 可以避免每次启动时的登录提示。

### 4. 配置 DeepSeek API
由于 DeepSeek 是开源的 Claude 兼容模型，我们可以使用它来替代：

#### 方案一：使用 DeepSeek API
```json
{
    "claudeCode.apiProvider": "deepseek",
    "claudeCode.apiKey": "sk-your-deepseek-api-key",
    "claudeCode.baseUrl": "https://api.deepseek.com",
    "claudeCode.model": "deepseek-chat"
}
```

#### 方案二：使用本地模型（推荐）
如果您有本地计算资源，可以使用 Ollama 运行 Claude 模型：

1. 安装 Ollama：
```bash
# Windows
winget install Ollama

# macOS
brew install ollama

# Linux
curl -fsSL https://ollama.com/install.sh | sh
```

2. 下载 Claude 模型：
```bash
ollama pull claude3
```

3. 配置 VS Code：
```json
{
    "claudeCode.apiProvider": "ollama",
    "claudeCode.baseUrl": "http://localhost:11434",
    "claudeCode.model": "claude3"
}
```

### 5. 验证配置
重启 VS Code，打开一个文件，尝试使用 Claude Code 的功能：
- 使用 `Ctrl+Shift+P` 打开命令面板
- 搜索 "Claude Code" 相关命令
- 或者直接在编辑器中使用 `/` 命令

## 📋 环境变量配置（可选）

您也可以通过环境变量来配置：

```bash
# 创建 .env 文件
CLAUDE_CODE_API_PROVIDER=deepseek
CLAUDE_CODE_API_KEY=your-api-key
CLAUDE_CODE_BASE_URL=https://api.deepseek.com
CLAUDE_CODE_MODEL=deepseek-chat
CLAUDE_CODE_DISABLE_LOGIN_PROMPT=true
```

## 🔍 常见问题

### Q: 为什么选择 DeepSeek 而不是官方 Claude？
A: 
- 无需注册 Anthropic 账户
- API 成本更低
- 开源模型，可本地部署
- 功能兼容性好

### Q: 如何获取 DeepSeek API Key？
1. 访问 [DeepSeek 官网](https://platform.deepseek.com/)
2. 注册账户
3. 在控制台创建 API Key

### Q: 提示 "Not authorized" 怎么办？
A: 
- 检查 API Key 是否正确
- 确认 API Key 是否有足够权限
- 检查网络连接是否正常

## 💡 最佳实践

1. **不要提交 API Key** 到版本控制
   - 使用环境变量
   - 加入 .gitignore

2. **定期更新 API Key**
   - 出于安全考虑，定期更换

3. **配置文件管理**
   - 不同环境使用不同配置
   - 使用配置文件模板

## 📚 参考资源

- [DeepSeek 官方文档](https://platform.deepseek.com/docs)
- [Claude Code GitHub](https://github.com/anthropics/claude-code)
- [Ollama 官方文档](https://ollama.com/docs)

---

*创建日期: 2026-05-25*
*学习进度: ✅ 已完成配置*