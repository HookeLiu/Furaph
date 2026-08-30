# Furaph-Plugin

Furaph 经 Shell 宿主协议接入的自治扩展能力与外部协议适配层。

## 定位

Plugin 用于承载经过治理的扩展能力，例如：

- 外部协议适配器；
- 可插拔工具或能力描述；
- 与 Shell 宿主协议对接的独立实现；
- 经授权的输入/输出格式转换。

IM ingress/outbox、引导员短上下文和渠道回执属于 IM Plugin；统一记忆可作为 built-in Plugin 自治建库。Plugin 不决定自然人授权或表达层话题。

Plugin **不负责**：

- 绕过 Furaph-Core 直接调用模型供应商或其他出站服务；
- 自行实现鉴权、路由、计价、usage/cost、预算或审计账本；
- 伪造 usage/cost、修改 Core 记账结果或隐藏失败；
- 默认获得宿主机文件、网络、进程、密钥或数据库权限；
- 假定插件代码天然可信并在主进程内任意执行。

## 依赖方向

```text
Plugin -> Shell 宿主协议 -> Core API/events
Shell  -> 表达层 Topic / 授权 / ContextPlan
Core   -> 受控上游与执行审计链路
```

Plugin 不静态依赖 Shell 私有实现。Shell 负责发现、注册、用户授权与编排；Core 负责执行准入、实际调用和执行审计。

## 开发

```bash
python -m pip install -e ".[test]"
python -m pytest -q
```
