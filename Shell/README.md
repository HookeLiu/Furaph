# Furaph-Shell

Furaph 的人机终端、表达层话题与 Agent 编排控制面。

## 定位

Shell 面向用户和运维者，负责：

- 对话与会话交互界面；
- 自然人、渠道绑定、信任圈角色和逐资源授权；
- 表达层 `ConversationTopic`、分支、消息修订、checkpoint/fork 与上下文预算；
- 不可变 `ContextPlan`/`RequestArtifact`、工具定义和模型路由请求；
- Plugin 的发现、注册、风险评估与宿主协议；
- Core turn、Agent 状态和流式事件的观察；
- 受控配置入口与运行状态展示；
- usage/cost、预算结果和审计事件的只读展示；
- 面向用户的错误、取消和终止提示。

Shell **不负责**：

- 直接调用 OpenAI、OpenRouter 或其他模型供应商；
- 供应商计价、权威 usage/cost、Core 执行硬上限和执行准入；
- 出站代理、failover、访问控制和 Core Agent 状态机；
- 绕过 Core 直接读写运行数据库、日志或密钥。

## 依赖方向

```text
用户/浏览器 ---------> Shell 编排 -> Core API / 事件流 -> 受控上游与记账
Plugin 宿主协议 ----->     |
                              -> 表达层 Topic / 授权 / ContextPlan
```

Shell 与 Core、Plugin 均通过显式、可版本化的契约交互，不通过 Python 包导入共享私有实现。Plugin 的业务意图由 Shell 编排后进入 Core；Core 独立验证授权快照和执行硬约束。

## 目标服务形态

Shell 将作为常驻 FastAPI/ASGI 服务运行，并自主维护独立 SQLite 数据库、artifact store、可靠 inbox/outbox、后台 worker、schema migration、备份与恢复。WebUI、CLI 和 Plugin 统一访问 Shell Service，不直接以本地文件或浏览器缓存裁决 Topic 与授权。

Core、Shell、Plugin 各自持有数据库，不共享表、不跨库双写。Shell 的领域状态、审计事件和待发送 outbox 在同一事务提交；Core 执行事实和 Plugin 渠道事实以幂等事件与 receipt 投影进入 Shell。

## 开发

```bash
python -m pip install -e ".[test]"
python -m pytest -q
```
