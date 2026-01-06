# OPML 测试用例模板

## ⚠️ OPML 格式规范（必须遵守）

生成 OPML 文件时，**必须遵守以下规范**以确保 XMind 正确解析：

| 规则 | 说明 | 错误示例 | 正确示例 |
|------|------|----------|----------|
| 禁止XML注释 | 不要使用 `<!-- -->` 注释 | `<!-- 模块1 -->` | 直接删除注释 |
| 转义双引号 | 属性值中的 `"` 必须转义 | `text="显示"hello""` | `text="显示&quot;hello&quot;"` |
| 转义尖括号 | 属性值中的 `<` `>` 必须转义 | `text="a<b>c"` | `text="a&lt;b&gt;c"` |
| 转义&符号 | 属性值中的 `&` 必须转义 | `text="A&B"` | `text="A&amp;B"` |
| 禁止emoji | 不要使用emoji，改用文字 | `text="状态🟢"` | `text="状态（绿色）"` |

**XML实体转义对照表：**

| 字符 | 实体编码 |
|------|----------|
| `"` | `&quot;` |
| `<` | `&lt;` |
| `>` | `&gt;` |
| `&` | `&amp;` |
| `'` | `&apos;` |

---

## 基础模板

```xml
<?xml version="1.0" encoding="UTF-8"?>
<opml version="2.0">
  <head>
    <title>{项目名称}测试用例</title>
    <dateCreated>{日期}</dateCreated>
    <expansionState>0,1,2,3,4,5,6,7,8</expansionState>
  </head>
  <body>
    <outline text="{项目名称}测试用例">
      <outline text="{模块名称}">
        <outline text="{用例名称}">
          <outline text="{前置条件}">
            <outline text="{执行步骤}">
              <outline text="{预期结果}">
                <outline text="{优先级}"/>
              </outline>
            </outline>
          </outline>
        </outline>
      </outline>
    </outline>
  </body>
</opml>
```

## 常见测试模块模板

### 编译构建测试

```xml
<outline text="编译构建测试">
  <outline text="{目标平台}编译成功验证">
    <outline text="已安装{工具链}和{目标}">
      <outline text="在{目录}执行 {编译命令}">
        <outline text="编译成功，无错误输出，生成目标产物">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### PRD UI/交互设计测试

```xml
<outline text="PRD UI/交互设计测试">
  <outline text="界面布局-{区域名称}显示正确">
    <outline text="应用已启动，进入{页面名称}">
      <outline text="观察{区域名称}的布局和显示">
        <outline text="{区域名称}正确显示在{位置}，包含{组件列表}">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="交互操作-{操作名称}响应正确">
    <outline text="应用处于{状态}，{组件}可见">
      <outline text="执行{操作}（点击/拖拽/输入）">
        <outline text="{预期响应}，界面{变化描述}">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 会话/连接管理测试

```xml
<outline text="会话管理测试-{阶段}">
  <outline text="{请求类型}请求正常处理">
    <outline text="{组件}处于{状态}状态">
      <outline text="发送{请求类型}请求（{参数}）">
        <outline text="返回{响应类型}响应，{验证点}，状态变为{新状态}">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 心跳/超时测试

```xml
<outline text="心跳超时检测">
  <outline text="{组件}处于Active状态，{参数}={值}">
    <outline text="超过{时间}未发送心跳，调用{检测方法}">
      <outline text="{计数器}增加，状态{变化描述}">
        <outline text="P0"/>
      </outline>
    </outline>
  </outline>
</outline>
```

### 功能测试

```xml
<outline text="功能测试">
  <outline text="{功能名称}-正常流程">
    <outline text="{前置条件描述}">
      <outline text="{操作步骤}">
        <outline text="{预期结果}">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 状态机测试

```xml
<outline text="{状态上下文}状态机测试">
  <outline text="状态转换-{起始状态}到{目标状态}">
    <outline text="{上下文}处于{起始状态}状态">
      <outline text="{触发条件/事件}">
        <outline text="状态变为{目标状态}，{附加验证}">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 边界值测试

```xml
<outline text="边界值测试">
  <outline text="{字段名称}-最大值边界">
    <outline text="{功能}正常可用">
      <outline text="输入{字段}={最大值}，执行{操作}">
        <outline text="{预期结果}">
          <outline text="P1"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="{字段名称}-超过最大值">
    <outline text="{功能}正常可用">
      <outline text="输入{字段}={最大值+1}，执行{操作}">
        <outline text="提示错误，{错误描述}">
          <outline text="P1"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 异常/错误处理测试

```xml
<outline text="错误处理测试">
  <outline text="{错误类型}错误-{触发条件}">
    <outline text="{组件}正常运行">
      <outline text="{触发错误的操作}">
        <outline text="返回{错误类型}错误，{错误处理描述}">
          <outline text="P1"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 配置测试

```xml
<outline text="{配置类}配置测试">
  <outline text="{配置项}配置-{场景}">
    <outline text="创建{配置类}实例">
      <outline text="设置{配置项}为{值}">
        <outline text="配置成功，{配置项}值为{值}{说明}">
          <outline text="P1"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 兼容性测试

```xml
<outline text="兼容性测试">
  <outline text="{平台/环境}兼容性验证">
    <outline text="在{平台/环境}上部署应用">
      <outline text="执行{核心功能}">
        <outline text="功能正常，无兼容性问题">
          <outline text="P1"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 集成测试

```xml
<outline text="集成测试">
  <outline text="{集成场景}">
    <outline text="{组件A}已完成，{组件B}已添加依赖">
      <outline text="执行 {集成命令/操作}">
        <outline text="{集成成功验证点}">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 端到端测试

```xml
<outline text="端到端测试">
  <outline text="{端到端场景}">
    <outline text="{测试客户端}与{设备/服务}建立连接">
      <outline text="执行{完整流程}">
        <outline text="所有步骤正确执行，{验证点}">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 资源限制测试

```xml
<outline text="内存与资源限制测试">
  <outline text="{限制项}验证">
    <outline text="{组件}配置{限制项}={限制值}">
      <outline text="尝试{超出限制的操作}">
        <outline text="{操作}失败，返回{错误类型}错误">
          <outline text="P1"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

## 优先级分配指南

### P0 场景（必须测试）

- 核心业务正向流程
- 编译/构建验证
- 关键状态转换
- 主要 API 正常调用
- 端到端关键路径
- PRD UI/交互核心功能
- 验收标准直接相关

### P1 场景（应该测试）

- 配置参数验证
- 异常/错误处理
- 边界条件
- 次要 API 调用
- 状态恢复
- 主题/语言切换

### P2 场景（可选测试）

- 辅助功能
- 日志/调试信息
- 性能优化验证
- 可选参数
- 稳定性测试
- 极端场景

## 测试设计方法

### 等价类划分
- 有效等价类：正常输入
- 无效等价类：异常输入

### 边界值分析
- 最小值、最小值+1
- 最大值、最大值-1
- 默认值

### 状态转换测试
- 覆盖所有状态
- 覆盖所有转换路径
- 测试无效转换

### 错误猜测
- 文件缺失
- 网络异常
- 权限不足
- 资源不足
