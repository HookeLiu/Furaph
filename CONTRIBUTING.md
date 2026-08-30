# CONTRIBUTING.md

## 提交前检查

```bash
python -m pytest -q
```

提交必须使用意图明确的 Conventional Commit 形式：

```text
<type>(<scope>): 中文表述的修改意图简介

(<body>)

(<footer>)
```

body部分虽然为可选，但如果涉及接口变化、功能修改或重要修复，必须在body中详细说明修改内容、原因及影响。

## 安全

禁止提交密钥、令牌、数据库、日志、缓存、用户敏感数据和未审计的第三方运行产物。
