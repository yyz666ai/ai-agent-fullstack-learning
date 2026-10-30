# 课程发现

## 用户目标
- 技术基础较少，需要从零解释概念、比喻、代码逻辑和可运行练习。
- 用户提供了第一章课件（`课件/第一章`）与完整项目（`ai-agent-fullstack-training`）。
- 每次教学后需要记录学习进度，供后续恢复。

## 课程结构（初步）
- 第一章课件主题：模型 API 与可控 Harness、流式输出、提示词工程、结构化输出、LLM Gateway、统一模型调用服务。
- 对应代码位于 `ai-agent-fullstack-training/course_code/week01`，从 `1-1` 到 `1-7`。
- 第二周开始包含工具运行时、MCP 和工具治理，说明第一章的目标是先搭好 Agent 的“模型调用基础设施”。

## 第一节要点
- 用户已纠正授课起点：应严格按 `1-1-从模型 API 到可控的 Agent Harness.pdf` 的知识顺序；课程代码目录编号仅用于匹配实践，不应改变 PPT 的讲解顺序。
- PPT 第 1 至 5 页是定位和工程动机；第一个具体技术知识点是第 6 页“Chat Completions 与 Responses”。下一次从此处开始。

## 已讲：Chat Completions 与 Responses
- Chat Completions 的核心请求形状是 `messages`，典型文本结果位于 `choices[0].message.content`；配套代码是 `week01/1-2/chat.py`。
- Responses 的核心是 `output` 项集合，除展示文本外，还可以用 item 类型区分 `message`、`function_call`、`reasoning`、`refusal` 等下一步事件；配套代码是 `week01/1-2/responses.py`。
- 二者不是新旧替代：多供应商兼容层通常优先以 Chat 为共同基线；新 Agent 若需要明确事件和多模态语义，再使用 Responses。
- 项目的 `modelAdapter.py` 将不同供应商的调用统一成 `ModelRequest -> ModelResult`；该抽象的目标是让上层 Loop 不依赖某一种 API 形状。注意 `dsAdapter.py` 将 DeepSeek Chat 的 `responses` 能力标为 False，因此不能假设课程示例中的 Responses 调用能对所有 OpenAI Compatible 供应商直接运行。
- 首个 Loop 位于 `week01/1-1/agent_loop_demo.py`：模型以 JSON 提出动作，代码解析为 `toolCall`，运行工具，将结果写回 `ctx.messages`，再调用模型直到模型给出普通文本。
- `eval_runner.py` 使用两个案例检查：是否选对工具、参数是否正确、最终答案是否包含期望词，体现“能跑”和“可验证”的差异。
- `sandbox_runner.py` 已在本机验证正常结果、超时和运行时错误三种返回；它是教学用最小隔离，不等同于生产级安全沙箱。
- 该最小 Loop 没有最大轮数、工具名白名单校验、结构化模型原生工具调用或可靠 JSON 解析；这些是课程后续将逐项补齐的工程边界。

## 资源
- 第一章讲义：`课件/第一章/第一章 学习笔记.md`
- 第一讲课件：`课件/第一章/1-1-从模型 API 到可控的 Agent Harness.pdf`
- 第一讲代码：`ai-agent-fullstack-training/course_code/week01/1-1/`

## 文字稿资料
- 用户新增了第一章的逐字稿 Markdown。后续每节应同时阅读对应 PPT、文字稿与课程代码，再进行由浅入深的讲解。
- 已识别的资料按顺序包括：`1-1 Chat Completions - Responses API.md`、`1-2模型参数、Token 与 Context Window.md`、`1-3 错误类型、异常处理与多模型调用基础.md`、3 份 Streaming 文字稿与 1 份 System Prompt 文字稿。
- `1-1` 文字稿明确了术语边界：SDK 是调用服务的客户端库；Chat/Responses 是 API 形态；换供应商应使用 Adapter，而不是把 Loop 绑定到 SDK。

## 练习环境发现
- 默认 `python3` 与桌面提供的 Python 都未安装 `openai` 包，练习环境需要隔离的虚拟环境和依赖安装步骤。
- 推荐把 API Key 存放在工作区 `练习/.env`，由练习脚本读取；不要把 Key 写进课程源码、VSCode 设置或 Git 追踪文件。

## 2026-09-14 - 第一、二章全景梳理
- 第一章（Week 01）先建立模型调用基础设施：API 形态和上下文、参数与预算、流式事件、Prompt 行为契约、Structured Output 协议、Gateway 与可部署服务。它解决的是“模型如何可靠地参与系统”。
- 第二章（Week 02）在第一章之上建立行动基础设施：Function Calling 的候选动作、Tool Runtime 的受控执行、MCP 外部能力接入、治理安全边界，以及 v2 的整合。它解决的是“模型提出的动作如何在不越权的前提下变成真实业务结果”。
- 对零基础学习者，不能直接把 1.7 或 2.5 当作首个实践；应先补足 Python 最小阅读能力和每一层的职责边界，再循序读取项目代码。练习目录和真实模型调用仍未创建或验证。
