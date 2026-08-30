# Furaph-Core

狐构（Furaph）基础执行与记录服务仓：AI Agent 执行基座、**统一 LLM 中继**、通信层会话、工具运行时与可审计账本。

> 项目处于初始化阶段。本 README 中的能力描述以已提交代码与 `CONTEXT.md` 验证记录为准，规划不等于已实现。

## 技术栈偏好

Python · FastAPI · httpx · SQLite · pydantic

工程偏好：模块化解耦、唯一真相源、全局一致性、人类可读可维护。

## 本地开发（占位）

```text
python -m venv .venv
.venv\Scripts\activate
pip install -e ".[dev]"
pytest
```

中继独立入口（实现后）：

```text
python -m furaph_core.gateway
```

配置：复制 `config.example.yaml` → `config.yaml`，用环境变量注入密钥。
