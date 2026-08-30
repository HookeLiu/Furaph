# AGENTS.md

## 1. 仓库定位

Furaph(狐构个人工程智能系统)的汇总实现(开源部分). 开发偏好 Python生态, 架构按模块化意图功能层级分拆为: **Core, Shell, Plugin** 3 大圈层, 每个圈层可能包含其各自的下属圈层嵌套。
整体规划为 **边界清晰、状态显式、上下文可追溯、结果可验证** 的系统。按 "圈层" 概念做解耦, 全面规避 "牵一发而动全身" 的维护困境, 程序与数据分离且每一个圈层各自内部闭环自洽。

## 2. 基本原则

1. **先读文档再改动**：开始任务前阅读本文件、`README.md` 和 `CONTEXT.md`；涉及子目录时继续查找并遵守更具体的 `AGENTS.md`。
2. **先摸底后实施**：先检查目录、Git 状态、现有文档和相关约束，再提出改动方案。
3. **最小变更**：只修改完成当前任务所需的文件，避免顺手重构或批量格式化。
4. **事实优先**：不把规划、推测或历史经验写成已实现事实；未知内容明确标注。
5. **边界清晰**：跨仓库引用必须说明目标、接口、版本或状态，不依赖隐式约定。
6. **可审计可回滚**：重要决策、接口变化和验证结果记录在 `CONTEXT.md` 或对应设计文档中。
7. **安全处理**：不得提交密钥、令牌、个人敏感数据、运行数据库、日志、缓存或临时文件。
8. **路径可移植**：代码与说明文档避免硬编码本机专有绝对路径（如盘符 `B:\...`、用户名、本机目录）。目录用约定名 + 相对位置（如各仓库工作区父目录）表述；确需举例时显式标注「本机示例」。

## 3. 文档维护

### README.md

面向项目使用者和协作者，描述项目定位、名称、目标、仓库规划、当前状态和文档入口。保持简洁，不记录详细过程日志。

### CONTEXT.md

面向持续开发，记录：

- 当前阶段和实际状态；
- 已确认决策及理由；
- 子仓库边界和跨仓依赖；
- 风险、未决问题和待办；
- 验证范围、结果和未覆盖部分。

上下文记录必须区分事实、计划、实验和未知。完成跨仓任务后，应同步更新相关状态和验证证据。

## 4. 变更流程

1. 阅读 `AGENTS.md`、`README.md`、`CONTEXT.md` 及相关目录规则。
2. 检查 `git status`、目录结构和目标文件现状。
3. 明确改动范围、影响面和回滚方式。
4. 采用精确编辑，避免覆盖无关内容。
5. 执行与改动匹配的检查：Markdown 链接、格式、脚本检查或项目测试。
6. 对照 diff 验收，确认没有密钥、临时文件或无关修改。
7. 更新 `CONTEXT.md`，记录决策和验证结果。
8. 使用清晰的 Git 提交信息：

```text
<type>(<scope>): 中文表述的修改意图简介
```

其中: `(scope)` 必须做归一化, 要么填写最相关的专有选项, 要么留空不填; **修改意图简介** 讲的是 **意图**(why/how) 而非流水账(what); 如果涉及多项改动, 则按逻辑意图分拆, 精准原子化提交.

`type` 必填选项：`docs`, `feat`, `fix`, `refactor`, `perf`, `test`, `chore`  
`(scope)` 可选选项：`core`, `shell`, `UI`, `DB`, `context`, `tools`, `profile`, `logging`, `cfg`, `CI`

## 5. 文件与目录规则

- 文档默认使用 UTF-8 编码和 Markdown 格式。
- 临时文件写入系统临时目录，不写入仓库。
- 新增目录或子仓库前，先说明职责、边界、依赖和独立验证方式。
- 规划中的仓库、链接和接口必须标注状态，不能伪装成已存在内容。
- 不得复制 CountBot 的运行数据、凭据、数据库、日志或未复核实现。

## 6. Git 规则

- 提交前检查 `git diff` 与 `git status`。
- 不修改或删除用户未授权的既有工作。
- 不执行破坏性 Git 操作，例如无确认的 `reset --hard`、强制推送或历史重写。
- 默认不主动推送远程仓库；需要推送时先确认目标分支和变更范围。
- 提交信息应说明修改意图，而不是只写“更新文档”。

## 7. 验收要求

文档或配置变更至少检查：

- 文件路径和链接是否正确；
- 规划状态是否与实际情况一致；
- 是否混入敏感信息或 CountBot 私有运行数据；
- `CONTEXT.md` 是否同步记录当前事实、待办和验证结果；
- Git diff 是否只包含本次任务相关内容。

如果无法验证某项，必须在结果中明确列出“未验证项”，不得默认视为通过。

## Shell Search Commands (Windows / PowerShell)

Use this order for text/file search in this repository:

1. Prefer `rg` (ripgrep) for recursive search and file listing.
2. Do not assume GNU `grep` options are available on Windows in this environment.

Reason:
- `grep` resolves to BusyBox here and does not support common GNU options such as `--exclude-dir` and `-P`.

### Safe Search Examples

```powershell
# Find TODO recursively (recommended)
rg -n "TODO" .

# File listing for agent workflows
rg --files -g "*.py"
```
