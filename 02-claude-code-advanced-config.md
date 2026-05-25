# 02 - Claude Code 高级配置与使用技巧

## 📝 学习目标
深入了解 Claude Code 的高级配置，包括多种使用场景和最佳实践。

## 🔧 详细配置方法

### 1. VS Code settings.json 完整配置

```json
{
    "claudeCode.disableLoginPrompt": true,
    "claudeCode.model": "claude-3-sonnet-20240229",
    "claudeCode.maxTokens": 4000,
    "claudeCode.temperature": 0.1,
    "claudeCode.apiProvider": "deepseek",
    "claudeCode.apiKey": "${env:DEEPSEEK_API_KEY}",
    "claudeCode.baseUrl": "https://api.deepseek.com",
    "claudeCode.timeout": 30000,
    "claudeCode.retryCount": 3,
    
    // 自定义快捷键
    "claudeCode.keybindings": {
        "explain": "ctrl+shift+e",
        "refactor": "ctrl+shift+r",
        "generate": "ctrl+shift+g"
    }
}
```

### 2. 环境变量配置

创建 `.env` 文件（加入 .gitignore）：
```env
# DeepSeek API 配置
DEEPSEEK_API_KEY=your-api-key-here
DEEPSEEK_BASE_URL=https://api.deepseek.com
DEEPSEEK_MODEL=deepseek-chat

# Claude Code 配置
CLAUDE_CODE_DISABLE_LOGIN_PROMPT=true
CLAUDE_CODE_MAX_TOKENS=4000
CLAUDE_CODE_TEMPERATURE=0.1
```

### 3. 本地模型配置（使用 Ollama）

如果不想使用 API，可以配置本地模型：

```json
{
    "claudeCode.apiProvider": "ollama",
    "claudeCode.baseUrl": "http://localhost:11434",
    "claudeCode.model": "claude3",
    "claudeCode.maxTokens": 2000,
    "claudeCode.temperature": 0.1
}
```

启动本地服务：
```bash
# 启动 Ollama 服务
ollama serve

# 下载模型（如果还没有）
ollama pull claude3
```

## 🚀 实用命令和快捷键

### 常用命令
- `/explain` - 解释代码
- `/refactor` - 重构代码
- `/generate` - 生成代码
- `/review` - 代码审查
- `/test` - 生成测试
- `/doc` - 生成文档

### 快捷键
- `Ctrl+Shift+P` - 打开命令面板
- `Ctrl+Shift+E` - 解释选中代码
- `Ctrl+Shift+R` - 重构选中代码
- `Ctrl+Shift+G` - 生成代码

## 💡 使用技巧

### 1. 提问的最佳实践

```
# 好的提问
"请帮我重构这个函数，使其更加模块化，并添加适当的注释。"
"解释这段代码的作用，并提供改进建议。"

# 避免的提问
"帮我改代码"
"看看这个"
```

### 2. 上下文管理

```python
# 在项目中使用上下文
"""
项目背景：这是一个使用 Flask 的 Web 应用
技术栈：Python, Flask, SQLAlchemy
当前文件：user/models.py
任务：优化 User 模型的查询性能
"""
```

### 3. 分步骤处理复杂任务

```
# 将复杂任务分解
1. 首先，分析现有代码结构
2. 然后，识别性能瓶颈
3. 接着，优化查询语句
4. 最后，添加测试用例
```

## 🐛 常见问题与解决方案

### 1. API 调用失败

**问题**：`Not authorized` 错误
```bash
# 解决方案
# 检查 API Key
echo $DEEPSEEK_API_KEY

# 测试 API 连接
curl -X POST "https://api.deepseek.com/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $DEEPSEEK_API_KEY" \
  -d '{"model": "deepseek-chat", "messages": [{"role": "user", "content": "Hello"}]}'
```

### 2. 模型响应慢

**解决方案**：
- 减少 `maxTokens`
- 增加 `temperature` 值
- 使用更小的模型
- 本地部署模型

### 3. 提示不工作

**检查清单**：
- [ ] VS Code 已重启
- [ ] settings.json 格式正确
- [ ] API Key 有效
- [ ] 网络连接正常

## 📈 性能优化

### 1. 配置优化
```json
// 高性能配置
{
    "claudeCode.maxTokens": 2000,
    "claudeCode.temperature": 0,
    "claudeCode.timeout": 15000,
    "claudeCode.retryCount": 1
}
```

### 2. 批量操作
```bash
# 使用脚本批量处理
find . -name "*.py" -exec claude code explain {} \;
```

## 🔄 工作流集成

### 1. Git 集成
```bash
# 提交前检查
git add .
claude code review --staged

# 创建 PR 前的代码审查
claude code review --branch feature/new-feature
```

### 2. CI/CD 集成
```yaml
# GitHub Actions 示例
- name: Code Review
  run: |
    npx claude code review --branch ${{ github.head_ref }}
```

## 📚 扩展资源

- [DeepSeek API 文档](https://platform.deepseek.com/docs)
- [Claude Code 官方文档](https://docs.anthropic.com/claude/docs)
- [Ollama 文档](https://ollama.com/docs)

---

*学习日期: 2026-05-25*
*难度等级: 🟡 中级*
*完成状态: ✅*