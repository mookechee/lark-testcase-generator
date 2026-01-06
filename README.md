# Lark Testcase Generator Plugin

从飞书项目单子自动生成 OPML 格式的 XMind 测试用例。

## 功能特性

- 自动读取飞书项目单子的描述和验收标准
- 自动读取技术设计文档
- 梳理用户操作流程和逻辑分支
- 生成结构化的 OPML 测试用例文件
- 支持导入 XMind、FreeMind 等思维导图工具

## 安装

### 方式一：直接使用（推荐）

Plugin 已安装在 `~/.claude/plugins/lark-testcase-generator/`

### 方式二：开发模式

```bash
claude --plugin-dir ~/.claude/plugins/lark-testcase-generator
```

## 前置要求

### 配置飞书 MCP 服务器

此 Plugin 依赖以下 MCP 服务器：

| MCP 服务器 | 用途 |
|-----------|------|
| `lark-prj-remote` | 读取飞书项目单子信息 |
| `lark-mcp-remote` | 读取飞书云文档内容 |

### 检查 MCP 配置

```bash
# 在 Claude Code 中运行
/mcp
```

### 配置 MCP 服务器

1. **获取飞书应用凭证**

   访问 [飞书开放平台](https://open.feishu.cn/) 创建应用并获取：
   - App ID
   - App Secret

2. **添加 MCP 服务器**

   ```bash
   # 飞书项目 MCP
   claude mcp add --transport stdio lark-prj-remote \
     --env LARK_APP_ID=YOUR_APP_ID \
     --env LARK_APP_SECRET=YOUR_APP_SECRET \
     -- npx -y @anthropic/claude-code-mcp-lark-prj

   # 飞书文档 MCP
   claude mcp add --transport stdio lark-mcp-remote \
     --env LARK_APP_ID=YOUR_APP_ID \
     --env LARK_APP_SECRET=YOUR_APP_SECRET \
     -- npx -y @anthropic/claude-code-mcp-lark
   ```

3. **或编辑配置文件**

   编辑 `~/.claude/settings.json`：

   ```json
   {
     "mcpServers": {
       "lark-prj-remote": {
         "command": "npx",
         "args": ["-y", "@anthropic/claude-code-mcp-lark-prj"],
         "env": {
           "LARK_APP_ID": "cli_xxxxxxxxxx",
           "LARK_APP_SECRET": "xxxxxxxxxxxxxxxxxx"
         }
       },
       "lark-mcp-remote": {
         "command": "npx",
         "args": ["-y", "@anthropic/claude-code-mcp-lark"],
         "env": {
           "LARK_APP_ID": "cli_xxxxxxxxxx",
           "LARK_APP_SECRET": "xxxxxxxxxxxxxxxxxx"
         }
       }
     }
   }
   ```

## 使用方法

### 命令方式

```bash
# 生成测试用例
/lark-testcase-generator:generate https://project.feishu.cn/uts5wn/story/detail/6596729761

# 检查 MCP 配置
/lark-testcase-generator:check-mcp
```

### 自然语言方式

直接向 Claude 描述需求，Skill 会自动触发：

```
帮我为这个飞书项目单子生成测试用例：
https://project.feishu.cn/xxx/story/detail/xxx
```

## 测试用例格式

每条测试用例采用链式结构：

```
用例名称
  └── 前置条件
        └── 执行步骤
              └── 预期结果
                    └── 优先级 (P0/P1/P2)
```

### 优先级说明

| 优先级 | 说明 |
|--------|------|
| P0 | 核心功能，必须测试 |
| P1 | 重要功能，应该测试 |
| P2 | 次要功能，可选测试 |

## 输出文件

默认输出路径：`~/Testcase/opml/{项目名}-testcase.opml`

OPML 文件可导入以下工具：
- XMind
- FreeMind
- MindManager
- 其他支持 OPML 格式的思维导图工具

## 目录结构

```
lark-testcase-generator/
├── .claude-plugin/
│   └── plugin.json              # Plugin 配置清单
├── commands/
│   ├── generate.md              # 生成测试用例命令
│   └── check-mcp.md             # 检查 MCP 配置命令
├── skills/
│   └── testcase-generator/
│       ├── SKILL.md             # Skill 定义
│       └── TEMPLATE.md          # OPML 模板
├── hooks/
│   └── hooks.json               # 钩子配置
└── README.md                    # 说明文档
```

## 常见问题

### Q: 提示 "MCP server not found"

A: 运行 `/lark-testcase-generator:check-mcp` 查看配置指南。

### Q: 无法读取飞书文档

A: 确保飞书应用已开启相关 API 权限，并且是文档的协作者。

### Q: OPML 文件导入 XMind 后格式错乱

A: 检查 OPML 文件编码是否为 UTF-8，确保无特殊字符。

## 更新日志

### v1.0.0 (2025-12-24)

- 初始版本
- 支持从飞书项目单子生成测试用例
- 支持读取技术设计文档
- 支持 OPML 格式输出
- MCP 配置检测和引导
