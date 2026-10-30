# 学习陪伴记录

## 2026-09-02 - 第一章第 1 节已讲解
- 已完成：定位和视觉核对 1-1 开营课件、核对第一章 26 页 Harness PDF、阅读并分层梳理 `agent_loop_demo.py`、`sandbox_runner.py`、`eval_runner.py` 与评测样例。
- 已验证：不需要 API Key 的教学练习成功复现了“模型提出工具调用 → 程序执行 → 结果回填 → 最终回答”；现有 Python 工具沙箱对成功、超时、运行时异常均返回结构化结果。
- 已讲解主题：课程全局地图、Agent 的最小组成、Harness/Loop/Eval 的职责边界、源码的执行链、最小 Demo 与生产工程的差距。
- 下一步：等用户运行无 Key 练习或提出问题后，进入第一章第 1.2 节：从模型 API 到可控的 Agent Harness。

## 2026-09-02 - Harness PPT：Chat Completions 与 Responses
- 已按用户指定的 PPT 顺序完成第一个技术点：Chat 的 messages 请求-响应模型与 Responses 的 output items 事件模型。
- 已对照 `week01/1-2/chat.py`、`responses.py` 与 Adapter 层代码；下一点是 PPT 第 8 页：messages 不是聊天记录，而是运行时上下文。

## 2026-09-02 - 学习资料与练习环境规划
- 已发现并阅读 Chat/Responses 对应的课堂文字稿；它补充了 SDK、API、请求字段和返回字段的术语解释。
- 已确认当前 Python 环境没有 `openai` SDK。待用户确认练习环境设计后，将创建隔离的 `练习/` 目录、虚拟环境、被忽略的 `.env` 配置和第一章可运行练习。

## 2026-09-14 - 第一、二章路线图已完成
- 已逐页核对第一章 6 份 PDF、第二章 5 份 PDF，阅读第一章完整学习笔记、已上传的字幕文字稿目录及 Week 01/Week 02 的代码结构。
- 已向用户说明：课程实际假定了一些 Python 和工程基础；后续将用“模型的大脑、Harness 的调度员、Tool 的手、Runtime 的安全检查员”的主线从零解释，不把先前一次 Chat/Responses 讲解当作用户必须已经掌握的前置。
- 正式下一步：从第一章 1.2 的 `messages` 和 `role` 开始，先补齐 Python 中列表、字典、函数与对象的最低阅读基础，再映射到 API 请求。

## 2026-09-14 - 第一章重新开始与课程项目更新
- 已安全执行老师项目的快进更新检查；`ai-agent-fullstack-training` 已与 `origin/main` 同步，未处理原有未追踪 Python 缓存目录。
- 已新增工作区内的 `第一章_零基础学习大纲.md`，把课件、文字稿、Week 01 代码和练习目标一一对应。
- 已重新完成第 0 节课程定位：LLM 负责提出候选，Tool 负责动作，Harness 管理状态与边界，Loop 负责多轮回写；下一讲进入 `messages` 与 `role`。

## 2026-09-14 - 第一章 messages 与 role 离线练习
- 已创建 `练习/第01章_模型API与Harness/01_messages与role/`；先写测试并确认因缺少实现而失败，再实现最小的 `build_messages()`，最后验证测试和示例程序通过。
- 已讲清：`messages` 是按顺序提供给模型的运行时上下文；`role` 表示消息职责。`system` 是开发者规则、`user` 是用户请求、`assistant` 是模型历史回答；role 本身不是权限边界。
- 已开始持续讲义 `我的专属Agent课程讲义.md`，记录用户问题、材料对应关系、教师解释、练习代码、运行结果、思考题与总结。
