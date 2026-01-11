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

### 接口/Handler 测试

```xml
<outline text="{Handler}测试">
  <outline text="{方法名}方法-{场景}">
    <outline text="{Handler}已实现，{资源条件}">
      <outline text="调用{方法名}({参数})">
        <outline text="返回{返回值}，{验证点}">
          <outline text="P1"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 错误处理测试

```xml
<outline text="错误处理测试">
  <outline text="{错误类型}错误-{触发条件}">
    <outline text="{组件}正常运行">
      <outline text="{触发错误的操作}">
        <outline text="返回{错误类型}错误">
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

### 软件/固件兼容性测试（重点）

```xml
<outline text="软件固件兼容性测试">
  <outline text="新软件+旧固件-{功能名称}验证">
    <outline text="设备运行旧版本固件V{X.X}，安装新版本软件V{Y.Y}">
      <outline text="执行{核心功能操作}">
        <outline text="{功能}正常工作，新旧版本协同正常">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="旧软件+新固件-{功能名称}验证">
    <outline text="设备运行新版本固件V{X.X}，安装旧版本软件V{Y.Y}">
      <outline text="执行{核心功能操作}">
        <outline text="{功能}正常工作，新旧版本协同正常">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="协议版本兼容-{协议名称}">
    <outline text="客户端使用协议V{X}，服务端使用协议V{Y}">
      <outline text="发起{通信操作}">
        <outline text="协议协商成功，通信正常">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="数据格式兼容-{数据类型}">
    <outline text="存在旧版本格式的{数据类型}数据">
      <outline text="使用新版本软件读取/处理该数据">
        <outline text="数据正确解析，功能正常">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="升级路径验证-从V{X}升级到V{Y}">
    <outline text="系统运行旧版本V{X}，数据正常">
      <outline text="执行升级到V{Y}的操作">
        <outline text="升级成功，数据完整迁移，功能正常">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="降级回滚验证-从V{Y}回滚到V{X}">
    <outline text="系统运行新版本V{Y}">
      <outline text="执行回滚到V{X}的操作">
        <outline text="回滚成功，系统恢复到旧版本状态">
          <outline text="P1"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="配置兼容-旧配置在新版本中的处理">
    <outline text="存在旧版本的配置文件">
      <outline text="使用新版本软件加载旧配置">
        <outline text="配置正确读取，缺省值正确填充">
          <outline text="P1"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 性能测试

```xml
<outline text="性能测试">
  <outline text="响应时间-{操作名称}">
    <outline text="系统处于正常负载状态">
      <outline text="执行{操作}，记录响应时间">
        <outline text="响应时间小于{X}ms，满足性能要求">
          <outline text="P1"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="并发处理-{并发数}用户同时操作">
    <outline text="系统正常运行">
      <outline text="{并发数}个用户同时执行{操作}">
        <outline text="所有请求正常处理，无错误，响应时间在可接受范围内">
          <outline text="P1"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="吞吐量-{操作名称}">
    <outline text="系统处于峰值负载状态">
      <outline text="持续发送{操作}请求，统计每秒处理数">
        <outline text="吞吐量达到{X}TPS，满足性能指标">
          <outline text="P1"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="资源占用-{场景名称}">
    <outline text="系统正常运行">
      <outline text="执行{操作场景}，监控CPU/内存/磁盘使用">
        <outline text="资源占用在合理范围内（CPU小于{X}%，内存小于{Y}MB）">
          <outline text="P2"/>
        </outline>
      </outline>
    </outline>
  </outline>
</outline>
```

### 安全测试

```xml
<outline text="安全测试">
  <outline text="权限控制-{功能名称}">
    <outline text="用户未登录或无权限">
      <outline text="尝试访问{受保护功能}">
        <outline text="访问被拒绝，返回权限不足提示">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="输入校验-{输入字段}">
    <outline text="功能正常可用">
      <outline text="在{输入字段}输入恶意内容（SQL注入/XSS/特殊字符）">
        <outline text="输入被正确过滤或拒绝，系统无异常">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="数据安全-{敏感数据}传输">
    <outline text="系统正常运行">
      <outline text="执行涉及{敏感数据}的操作，抓包分析">
        <outline text="{敏感数据}已加密传输，无法被窃取">
          <outline text="P0"/>
        </outline>
      </outline>
    </outline>
  </outline>
  <outline text="会话安全-会话劫持防护">
    <outline text="用户已登录">
      <outline text="尝试使用过期/伪造的会话令牌访问">
        <outline text="访问被拒绝，要求重新认证">
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
- 新旧软件/固件核心功能兼容
- 权限控制和输入校验（安全相关）

### P1 场景（应该测试）

- 配置参数验证
- 异常/错误处理
- 边界条件
- 次要 API 调用
- 状态恢复
- 升级/降级路径验证
- 协议版本兼容
- 数据格式兼容
- 性能基准测试（响应时间、并发处理）
- 会话安全

### P2 场景（可选测试）

- 辅助功能
- 日志/调试信息
- 性能优化验证
- 可选参数
- 稳定性测试
- 极端场景
- 资源占用监控
