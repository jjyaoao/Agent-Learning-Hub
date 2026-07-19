# Agent Learning Hub

A curated AI Agent learning roadmap for people who want to build useful, reliable agents instead of collecting random links.

这个仓库只维护一个核心展示面：README。目标是把社区里优秀分享、官方博客、论文、开源项目和真实工程经验，整理成一份可以照着执行的 AI Agent 学习 todo list。

## Maintainer

Curated by [陈思州](https://github.com/jjyaoao) (Datawhale 成员) <a href="https://www.xiaohongshu.com/user/profile/67b9cc34000000000e013517" target="_blank"><img alt="Static Badge" src="https://img.shields.io/badge/Rednote-小红书-e93c49"></a>

## How To Use

- 如果你是新手：按「Learning Todo List」从上到下做，每完成一项就打勾。
- 如果你已经会 LLM 应用：从 Stage 2 或 Stage 3 开始，重点补 Agent loop、工具调用、评测和工程化。
- 如果你想做项目：直接看「Project Ladder」，每一档做一个可运行作品。
- 如果你只想找资料：看「Curated Resources」，优先读官方文档和经典论文。

## What To Learn Now

Agent 领域变化很快。当前更值得投入的不是老式“角色扮演多 agent 框架”，而是这些更贴近真实生产力的方向：

| Priority | Learn | Why |
| --- | --- | --- |
| 1 | Claude Code / Codex-style coding agents | 真实代码库、shell、文件编辑、测试、权限、上下文压缩，是最好的 agent 工程样本。 |
| 2 | Agent harness engineering | agent 的能力很大一部分来自 harness：工具协议、权限、状态、反馈、回放、CI、评测。 |
| 3 | OpenClaw / Hermes-style personal agents | 长运行、本地优先、跨应用、记忆、skills、消息入口，更像“个人操作系统”。 |
| 4 | Skills / MCP / A2A / ACP | skills 负责能力复用，MCP 连接工具，A2A 连接 agent，ACP 连接宿主应用。 |
| 5 | Evaluation and safety | 没有 eval、trace、权限边界的 agent 只能算 demo。 |

不建议把精力重押在已经泛化成模板的老式 crew/role-play 框架上。它们可以了解，但不应成为主线。

## Learning Todo List

### Stage 0: Understand What An Agent Is

- [ ] 区分 chatbot、workflow、agent、multi-agent。
- [ ] 理解 agent 的基本循环：observe -> think -> act -> observe。
- [ ] 明白什么时候不该用 agent：任务可预测、流程稳定、普通脚本能解决时，agent 反而增加不确定性。
- [ ] 读完 [Anthropic: Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)。
- [ ] 读完 [OpenAI: A practical guide to building agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)。

产出：写一页短笔记，回答「我的场景为什么需要 agent，而不是普通 workflow？」

### Stage 1: Build A Minimal Agent Loop

- [ ] 会用一个 LLM API 完成普通对话。
- [ ] 会让模型输出结构化 JSON。
- [ ] 会定义一个工具函数，例如 search、calculator、read_file。
- [ ] 会解析模型的 tool call / function call。
- [ ] 会执行工具，并把工具结果喂回模型。
- [ ] 会给 agent loop 加最大步数、超时和错误处理。

推荐阅读：

- [OpenAI Function Calling](https://platform.openai.com/docs/guides/function-calling)
- [Gemini API Function Calling](https://ai.google.dev/gemini-api/docs/function-calling)
- [Claude Tool Use](https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/overview)

产出：一个 50-150 行的最小 agent，可以选择工具、执行工具、返回最终答案。

### Stage 2: Learn Tool Use, RAG, And Memory

- [ ] 会做检索增强生成：chunk、embed、retrieve、answer with citations。
- [ ] 会把搜索、数据库、文件、浏览器、代码执行接成工具。
- [ ] 会区分短期上下文、会话记忆、长期记忆。
- [ ] 会处理工具失败、空结果、重复调用、幻觉引用。
- [ ] 会让 agent 在回答里给出来源或证据。

推荐阅读：

- [LlamaIndex Agents](https://docs.llamaindex.ai/en/stable/use_cases/agents/)
- [LangChain Docs](https://docs.langchain.com/)
- [Gemini API Code Execution](https://ai.google.dev/gemini-api/docs/code-execution)
- [Model Context Protocol](https://modelcontextprotocol.io/)

开源项目参考：

| Project | Why It Fits Stage 2 |
| --- | --- |
| [GPT Researcher](https://github.com/assafelovic/gpt-researcher) | 最接近“资料研究助手”的成品：搜索、抓取、筛选、引用、生成长报告。 |
| [Open Deep Research](https://github.com/langchain-ai/open_deep_research) | LangGraph 写的 deep research 示例，适合学多轮搜索、状态管理和引用输出。 |
| [STORM](https://github.com/stanford-oval/storm) | Stanford OVAL 的研究写作系统，适合学 outline、question asking、多视角资料综合。 |
| [Khoj](https://github.com/khoj-ai/khoj) | 个人 second brain，适合学本地文档、网页、语义搜索和长期记忆。 |
| [Onyx](https://github.com/onyx-dot-app/onyx) | 企业级 RAG/search assistant，适合学 connectors、hybrid search、权限和生产化。 |
| [AnythingLLM](https://github.com/Mintplex-Labs/anything-llm) | 本地 RAG + agents 产品，适合初学者快速理解完整应用形态。 |
| [RAGFlow](https://github.com/infiniflow/ragflow) | 文档理解型 RAG 引擎，适合学 ingestion、chunking、retrieval、grounded answer。 |
| [mem0](https://github.com/mem0ai/mem0) | 记忆层组件，适合学如何给 agent 加长期 memory。 |
| [Letta](https://github.com/letta-ai/letta) | 面向 stateful agents 的 memory/context 平台，适合学上下文管理。 |

产出：一个资料研究助手，输入主题后自动搜索、筛选、总结并输出引用链接。

### Stage 3: Study One Modern Agent Harness

先选一个现代 agent 系统学深。这里的重点不是“框架 API 怎么调”，而是它如何组织工具、上下文、权限、状态、日志、子任务和反馈。

| System | Best For | Learn This If You Want To |
| --- | --- | --- |
| [Claude Code Docs](https://code.claude.com/docs/en/overview) | Coding agent product | 学真实 coding agent 的 CLI、工具、权限、hooks、subagents、MCP。 |
| [learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | From-scratch agent harness | 从 0 到 1 复刻 Claude Code-like harness。 |
| [claw0](https://github.com/shareAI-lab/claw0) | From-scratch OpenClaw gateway | 从 agent loop 一路构建 session、channel、gateway、memory、heartbeat、delivery、resilience、concurrency。 |
| [hello-agents](https://github.com/datawhalechina/hello-agents) | Chinese agent tutorial | 从零开始构建智能体，适合系统补 Agent 原理与实践。 |
| [OpenClaw](https://github.com/openclaw/openclaw) | Local-first personal agent | 学本地长运行 agent、skills、消息入口、系统工具和安全边界。 |
| [Hermes Agent](https://github.com/NousResearch/hermes-agent) | Self-hosted growing agent | 学长期记忆、skills、toolsets、多平台消息网关和迁移能力。 |
| [CyberClaw](https://github.com/ttguy0707/CyberClaw) | Transparent agent architecture | 学全行为审计、两段式安全调用、双水位记忆和心跳任务。 |
| [LangGraph](https://langchain-ai.github.io/langgraph/) | Stateful graph orchestration | 学状态图、可恢复执行和可控编排。 |

- [ ] 读懂一个 agent harness 的目录结构。
- [ ] 找出它的 agent loop、tool registry、permission gate、session store、context compaction。
- [ ] 跑通它的最小示例，并加一个你自己的工具。
- [ ] 观察一次完整 trace，解释每一步为什么发生。
- [ ] 把同一个任务分别用「裸 agent loop」和「harness」实现，对比差异。

产出：一个可调试的 agent harness demo，包含 README、运行步骤、示例输入输出和失败记录。

### Stage 4: Multi-Agent Is Coordination, Not Magic

- [ ] 理解 planner / executor / reviewer / critic / router 等常见角色。
- [ ] 学会用 supervisor 或 graph 管理多 agent，而不是让 agent 随便聊天。
- [ ] 会定义每个 agent 的职责边界、输入输出 schema、停止条件。
- [ ] 会处理循环、争论、任务漂移、上下文膨胀。
- [ ] 会判断什么时候单 agent 更好。

推荐阅读：

- [Claude Code Subagents](https://code.claude.com/docs/en/sub-agents)
- [Claude Code Hooks](https://code.claude.com/docs/en/hooks)
- [Google Agent Development Kit](https://google.github.io/adk-docs/)
- [Agent2Agent Protocol](https://a2a-protocol.org/latest/specification/)
- [Agent Client Protocol](https://agentclientprotocol.com/)

产出：一个小型多 agent 系统，例如 research -> write -> review -> revise。

### Stage 5: Learn Skills, Protocols, And Capability Packaging

现代 agent 的能力不只来自模型和工具，也来自可复用的 skills。一个好的 skill 像一份小型操作手册：告诉 agent 什么时候使用、怎么使用、需要哪些脚本/资源、如何验证结果。

- [ ] 理解 Skill 和 Tool 的区别：tool 是可调用接口，skill 是可复用流程知识。
- [ ] 理解 Skill 和 Prompt 的区别：prompt 通常是一次性指令，skill 是可发现、可版本化、可分发的能力包。
- [ ] 理解 Skill 和 MCP 的区别：MCP 接入外部工具/数据源，skill 告诉 agent 如何完成一类任务。
- [ ] 阅读 Claude Code Skills 的文件结构和触发机制。
- [ ] 阅读 OpenClaw Skills 的加载、作用域和安全边界。
- [ ] 写一个最小 `SKILL.md`，包含 name、description、何时使用、步骤、验收标准。
- [ ] 给 skill 加一个脚本或模板文件，并说明 agent 什么时候才需要加载它。
- [ ] 给 skill 写一个 smoke test，验证它是否真的提升任务成功率。

推荐阅读：

- [Claude Code Skills](https://code.claude.com/docs/en/skills)
- [Claude Agent Skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills)
- [Claude Code Agent SDK Skills](https://code.claude.com/docs/en/agent-sdk/skills)
- [OpenClaw Skills](https://github.com/openclaw/openclaw/blob/main/docs/tools/skills.md)
- [Model Context Protocol](https://modelcontextprotocol.io/)
- [Agent2Agent Protocol](https://a2a-protocol.org/latest/specification/)
- [Agent Client Protocol](https://agentclientprotocol.com/)

产出：一个可复用 skill，例如 code-review、research-report、migration-helper、pdf-extraction 或 release-note-writer。

### Stage 6: Browser And Computer-Use Agents

- [ ] 理解 browser agent 和普通 API tool 的区别。
- [ ] 会用 Playwright 或 browser-use 做网页观察和点击。
- [ ] 会给浏览器操作加安全限制：不登录敏感账号、不越权、不绕过平台规则。
- [ ] 会处理页面变化、弹窗、加载失败、元素定位失败。
- [ ] 会记录截图、DOM、动作日志，方便复盘。

推荐阅读：

- [Claude Computer Use](https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/computer-use-tool)
- [browser-use](https://github.com/browser-use/browser-use)
- [WebArena](https://arxiv.org/abs/2307.13854)
- [VisualWebArena](https://arxiv.org/abs/2401.13649)

产出：一个只操作公开网页的 browser agent，例如打开网页、提取信息、生成摘要。

### Stage 7: Evaluation, Observability, And Safety

- [ ] 为 agent 准备固定测试集，而不是只看 demo。
- [ ] 记录成功率、失败原因、工具调用次数、成本、延迟。
- [ ] 会看 trace，知道失败发生在 prompt、工具、检索、模型还是状态管理。
- [ ] 给危险工具加人工确认，例如发邮件、删文件、付款、发布内容。
- [ ] 了解 prompt injection、data exfiltration、tool abuse 等风险。
- [ ] 会用回归测试防止 prompt 或工具改动后能力退化。

推荐阅读：

- [OpenAI Evals](https://platform.openai.com/docs/guides/evals)
- [OpenAI Agent platform](https://openai.com/agent-platform/)
- [LangSmith](https://docs.smith.langchain.com/)
- [AgentBench](https://arxiv.org/abs/2308.03688)
- [SWE-bench](https://arxiv.org/abs/2310.06770)

产出：一个 agent eval 表格，至少包含 20 个任务、期望结果、实际结果、失败分类。

### Stage 8: Ship A Real Agent

- [ ] 有明确用户、明确任务、明确成功标准。
- [ ] 有日志、trace、错误重试、超时、成本上限。
- [ ] 有权限边界和人工确认机制。
- [ ] 有部署方式：CLI、Web app、Slack bot、GitHub Action 或后台任务。
- [ ] 有 README：怎么运行、怎么配置 key、怎么扩展工具、有哪些限制。

产出：一个别人能 clone 下来跑的 agent 项目。

## Project Ladder

| Level | Project | What You Learn |
| --- | --- | --- |
| 1 | Calculator Agent | 最小 tool call loop |
| 2 | Web Research Agent | 搜索、筛选、引用、总结 |
| 3 | PDF QA Agent | RAG、chunk、retrieval、citation |
| 4 | Coding Review Agent | 读取 diff、风险排序、测试建议 |
| 5 | Browser Agent | 页面观察、点击、提取、失败恢复 |
| 6 | Claude Code-like Nano Agent | shell、文件编辑、权限、session、compact |
| 7 | OpenClaw-like Gateway | channel、routing、session、memory、heartbeat、delivery |
| 8 | Reusable Skill Pack | SKILL.md、脚本、模板、触发条件、smoke test |
| 9 | Multi-Agent Writer | planner、writer、reviewer 协作 |
| 10 | Personal Agent | OpenClaw/Hermes-style 记忆、skills、消息入口 |
| 11 | Production Harness | evals、trace、权限、CI、runner、回放 |

## Curated Resources

### Official Guides And Blogs

| Resource | Why It Matters |
| --- | --- |
| [Anthropic: Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) | Agent 设计入门必读，讲清 workflow 和 agent 的边界。 |
| [Claude Code Overview](https://code.claude.com/docs/en/overview) | 当前最值得研究的 coding agent 产品文档入口。 |
| [Claude Code Subagents](https://code.claude.com/docs/en/sub-agents) | 学任务拆分、上下文隔离、专用子代理。 |
| [Claude Code Hooks](https://code.claude.com/docs/en/hooks) | 学如何拦截、校验和扩展 agent 行为。 |
| [Claude Code GitHub Actions](https://docs.claude.com/en/docs/claude-code/github-actions) | 学 coding agent 如何进入 PR / issue 工作流。 |
| [Claude Code Advanced Patterns](https://resources.anthropic.com/hubfs/Claude%20Code%20Advanced%20Patterns_%20Subagents%2C%20MCP%2C%20and%20Scaling%20to%20Real%20Codebases.pdf) | Anthropic 官方材料，覆盖 subagents、MCP 和真实代码库扩展。 |
| [OpenAI: A practical guide to building agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/) | 面向产品和工程团队的 agent 落地指南。 |
| [OpenAI: New tools for building agents](https://openai.com/index/new-tools-for-building-agents/) | Responses API、Agents SDK、工具和 tracing 的官方介绍。 |
| [OpenAI Agents SDK](https://platform.openai.com/docs/guides/agents-sdk/) | OpenAI 原生 agent 开发入口。 |
| [Claude Tool Use](https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/overview) | Claude 工具调用机制。 |
| [Claude Computer Use](https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/computer-use-tool) | 电脑操作类 agent 的官方参考。 |
| [Gemini Function Calling](https://ai.google.dev/gemini-api/docs/function-calling) | Gemini 工具调用官方文档。 |
| [Gemini Code Execution](https://ai.google.dev/gemini-api/docs/code-execution) | Gemini 代码执行工具。 |
| [Google Agent Development Kit](https://google.github.io/adk-docs/) | Google 的 agent 开发框架。 |
| [Model Context Protocol](https://modelcontextprotocol.io/) | Agent 连接工具和数据源的重要协议。 |

### Project Map

项目不要按 star 数乱读，建议按学习目的分层：

| Layer | Study These | Learn |
| --- | --- | --- |
| Build From Scratch | [learn-claude-code](https://github.com/shareAI-lab/learn-claude-code), [claw0](https://github.com/shareAI-lab/claw0), [hello-agents](https://github.com/datawhalechina/hello-agents) | agent loop、tool registry、session、context compaction、gateway、trace、subagents。 |
| Personal / Always-On Agents | [OpenClaw](https://github.com/openclaw/openclaw), [Hermes Agent](https://github.com/NousResearch/hermes-agent), [CyberClaw](https://github.com/ttguy0707/CyberClaw) | 长运行、skills、记忆、消息入口、权限、安全审计。 |
| Coding Agents | [Claude Code](https://code.claude.com/docs/en/overview), [OpenAI Codex](https://github.com/openai/codex), [OpenCode](https://github.com/opencode-ai/opencode), [OpenHands](https://github.com/All-Hands-AI/OpenHands), [SWE-agent](https://github.com/SWE-agent/SWE-agent), [pi](https://github.com/earendil-works/pi) | 真实代码库编辑、shell、测试、sandbox、PR 工作流。 |
| Agent Harness / SuperAgent Runtime | [DeerFlow](https://github.com/bytedance/deer-flow), [LangGraph](https://langchain-ai.github.io/langgraph/) | 长任务执行、sandbox、memory、skills、subagents、message gateway、trace。 |
| Deep Research / RAG Agents | [GPT Researcher](https://github.com/assafelovic/gpt-researcher), [Open Deep Research](https://github.com/langchain-ai/open_deep_research), [LlamaIndex](https://docs.llamaindex.ai/) | 搜索、抓取、检索、rerank、引用、报告生成。 |
| Tutorial Encyclopedias | [GenAI_Agents](https://github.com/NirDiamant/GenAI_Agents), [hello-agents](https://github.com/datawhalechina/hello-agents), [smolagents](https://github.com/huggingface/smolagents), [agents-towards-production](https://github.com/NirDiamant/agents-towards-production) | 横向看 ReAct、Plan-and-Execute、Multi-Agent、production patterns。 |
| Browser / Multimodal Agents | [browser-use](https://github.com/browser-use/browser-use), [UI-TARS-desktop](https://github.com/bytedance/UI-TARS-desktop) | 浏览器/桌面操作、视觉理解、动作空间、失败恢复。 |

### Skills, Protocols, And Tooling

| Concept | Learn From | What It Solves |
| --- | --- | --- |
| Skills | [Claude Code Skills](https://code.claude.com/docs/en/skills), [OpenClaw Skills](https://github.com/openclaw/openclaw/blob/main/docs/tools/skills.md) | 把一类任务的流程知识、脚本、模板和验收标准打包成可复用能力。 |
| MCP | [Model Context Protocol](https://modelcontextprotocol.io/) | 让 agent 标准化连接外部工具、数据源和服务。 |
| A2A | [Agent2Agent Protocol](https://a2a-protocol.org/latest/specification/) | 让不同 agent 之间发现、通信和协作。 |
| ACP | [Agent Client Protocol](https://agentclientprotocol.com/) | 让编辑器、终端、IDE、宿主应用和 agent 之间形成统一接口。 |
| Skill Quality | [SWE-Skills-Bench](https://arxiv.org/abs/2603.15401), [Agent Skills analysis](https://arxiv.org/abs/2602.08004), [SkillOpt](https://github.com/microsoft/SkillOpt) | 评估、优化和验证 skills 是否真的提升成功率，而不是制造新的 prompt 噪声。 |

### Modern Agent Systems

| System | Why It Is Useful |
| --- | --- |
| [Claude Code](https://code.claude.com/docs/en/overview) | 学 coding agent 的产品化形态：shell、文件、权限、hooks、subagents、MCP。 |
| [learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | 从零构建 Claude Code-like nano agent，适合理解 harness engineering。 |
| [claw0](https://github.com/shareAI-lab/claw0) | 从零构建 OpenClaw-like agent gateway，覆盖 channel、routing、session、memory、delivery、concurrency。 |
| [hello-agents](https://github.com/datawhalechina/hello-agents) | 中文智能体系统教程，适合从零开始补齐 Agent 原理与实践。 |
| [OpenClaw](https://github.com/openclaw/openclaw) | 本地优先的个人 agent，适合研究长运行 agent 和系统级工具调用。 |
| [Hermes Agent](https://github.com/NousResearch/hermes-agent) | 自托管、长期记忆、skills、消息网关和 toolsets。 |
| [CyberClaw](https://github.com/ttguy0707/CyberClaw) | 透明可控 agent 架构，适合研究审计、两段式执行和安全边界。 |
| [DeerFlow](https://github.com/bytedance/deer-flow) | 字节开源 long-horizon SuperAgent harness。2.0 主分支是从头重写的通用 agent runtime，适合研究 sandbox、memory、skills、subagents、message gateway 和长任务执行；原 Deep Research 框架在 1.x 分支。 |
| [smolagents](https://github.com/huggingface/smolagents) | Hugging Face 轻量 agent 框架，CodeAgent 思路值得研究。 |
| [LangGraph](https://langchain-ai.github.io/langgraph/) | 状态图和可控 agent 编排，仍然值得作为工程基础学习。 |
| [Qwen-Agent](https://github.com/QwenLM/Qwen-Agent) | 国产模型生态里的工具调用、RAG、MCP agent 框架。 |
| [Pydantic AI](https://pydantic.dev/docs/ai/core-concepts/agent/) | 类型安全和结构化输出，适合生产 Python agent。 |
| [pi](https://github.com/earendil-works/pi) | AI agent toolkit（TypeScript），含 coding agent CLI、agent core、统一多提供商 LLM API 和 TUI 库，支持自扩展。 |

### Legacy Or Optional Frameworks

这些项目仍有参考价值，但不建议作为当前学习主线。

| Framework | Note |
| --- | --- |
| [CrewAI](https://docs.crewai.com/) | 可了解 role/task/crew 抽象，但很多场景已经被更强的 coding agent / harness 形态覆盖。 |
| [AutoGen](https://microsoft.github.io/autogen/) | 多 agent 对话框架经典项目，适合了解历史和论文，不必重押。 |
| [LangChain Agents](https://docs.langchain.com/) | 生态仍重要，但建议重点转向 LangGraph 和具体工程模式。 |

### Papers

| Paper | Topic |
| --- | --- |
| [ReAct](https://arxiv.org/abs/2210.03629) | Reasoning + acting 的基础范式。 |
| [Toolformer](https://arxiv.org/abs/2302.04761) | 模型学习何时调用工具。 |
| [Reflexion](https://arxiv.org/abs/2303.11366) | 语言反馈和自我改进。 |
| [Generative Agents](https://arxiv.org/abs/2304.03442) | 记忆、反思、规划驱动的模拟 agent。 |
| [Voyager](https://arxiv.org/abs/2305.16291) | 开放世界中的长期学习 agent。 |
| [AutoGen](https://arxiv.org/abs/2308.08155) | 多 agent 对话框架。 |
| [AgentBench](https://arxiv.org/abs/2308.03688) | Agent 能力评测。 |
| [WebArena](https://arxiv.org/abs/2307.13854) | 真实网页环境下的 agent benchmark。 |
| [SWE-bench](https://arxiv.org/abs/2310.06770) | 真实 GitHub issue 修复评测。 |
| [SWE-agent](https://arxiv.org/abs/2405.15793) | 软件工程 agent 的 agent-computer interface。 |
| [Dive into Claude Code](https://arxiv.org/abs/2604.14228) | 从系统设计角度分析 Claude Code 这类 coding agent 的 harness、权限、压缩和扩展机制。 |
| [AI Harness Engineering](https://arxiv.org/abs/2605.13357) | 把 harness 作为 agent 能力来源来研究。 |
| [Configuring Agentic AI Coding Tools](https://arxiv.org/abs/2602.14690) | 对 Claude Code、Codex、Gemini、Cursor 等 coding tools 的配置机制分析。 |
| [Your Agent, Their Asset](https://arxiv.org/abs/2604.04759) | OpenClaw 等本地 agent 的真实安全风险分析。 |

### GitHub Repositories

| Repo | Why It Is Useful |
| --- | --- |
| [datawhalechina/hello-agents](https://github.com/datawhalechina/hello-agents) | 中文智能体系统教程，从零开始构建智能体。 |
| [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | Bash is all you need，从 0 到 1 学 Claude Code-like agent harness。 |
| [shareAI-lab/claw0](https://github.com/shareAI-lab/claw0) | 从 0 到 1 学 OpenClaw-like gateway，10 个渐进章节覆盖 agent loop 到 concurrency。 |
| [openclaw/openclaw](https://github.com/openclaw/openclaw) | 研究本地个人 agent、skills、长运行任务、系统工具和权限边界。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 研究自托管 agent、长期记忆、skills、toolsets、多平台消息网关。 |
| [ttguy0707/CyberClaw](https://github.com/ttguy0707/CyberClaw) | 研究透明 agent、安全审计、两段式执行、双水位记忆和心跳任务。 |
| [bytedance/deer-flow](https://github.com/bytedance/deer-flow) | 2.0 是通用 long-horizon SuperAgent harness，适合学习沙箱、memory、skills、subagents、message gateway 和产物生成；Deep Research 代码看 1.x 分支。 |
| [NirDiamant/GenAI_Agents](https://github.com/NirDiamant/GenAI_Agents) | 综合教程库，适合横向比较 ReAct、Plan-and-Execute、Multi-Agent 等实现方式。 |
| [NirDiamant/agents-towards-production](https://github.com/NirDiamant/agents-towards-production) | production-grade agent 教程库，适合补工程化组件。 |
| [huggingface/smolagents](https://github.com/huggingface/smolagents) | 轻量 CodeAgent 风格框架，适合研究“让模型写代码执行动作”的范式。 |
| [openai/codex](https://github.com/openai/codex) | OpenAI 开源 coding agent CLI，适合研究 sandbox、approval、CLI 产品形态。 |
| [opencode-ai/opencode](https://github.com/opencode-ai/opencode) | 终端优先的开源 coding agent，适合对照 Claude Code / Codex。 |
| [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) | 状态图和可控 agent 编排。 |
| [openai/openai-agents-python](https://github.com/openai/openai-agents-python) | OpenAI Agents SDK Python。 |
| [QwenLM/Qwen-Agent](https://github.com/QwenLM/Qwen-Agent) | Qwen 生态 agent 框架。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 浏览器 agent 实战。 |
| [bytedance/UI-TARS-desktop](https://github.com/bytedance/UI-TARS-desktop) | 多模态桌面 agent stack，适合研究视觉 UI 操作。 |
| [SWE-agent/SWE-agent](https://github.com/SWE-agent/SWE-agent) | 软件工程 agent。 |
| [All-Hands-AI/OpenHands](https://github.com/All-Hands-AI/OpenHands) | 开源 coding agent。 |
| [microsoft/ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners) | 系统化入门课程。 |
| [jjyaoao/HelloAgents](https://github.com/jjyaoao/HelloAgents) | 基于 OpenAI 原生 API 的生产级多智能体框架，覆盖 ToolResponse、上下文工程、会话持久化、子代理、TraceLogger 等。 |
| [earendil-works/pi](https://github.com/earendil-works/pi) | TypeScript 写的 AI agent toolkit，含 pi-coding-agent CLI、pi-agent-core 运行时、pi-ai（统一多提供商 LLM API）、pi-tui（终端 UI 库），支持 Slack 机器人和 vLLM pods。 |

### Thoughtful Blogs

| Blog | Why It Is Useful |
| --- | --- |
| [Lilian Weng: LLM Powered Autonomous Agents](https://lilianweng.github.io/posts/2023-06-23-agent/) | 经典长文，系统整理 agent 架构、记忆、规划和工具使用。 |
| [Simon Willison: AI/LLM writing](https://simonwillison.net/tags/llms/) | 非常务实的 LLM 工程观察，适合补工程直觉。 |
| [LangChain Blog](https://blog.langchain.com/) | LangGraph、LangSmith、agent 工程实践。 |
| [Google Developers Blog: ADK](https://developers.googleblog.com/agent-development-kit-easy-to-build-multi-agent-applications/) | Google ADK 官方发布文章。 |

### Claude Code Study Path

Claude Code 是当前最值得拆解的 coding agent 产品之一。推荐按“官方文档 -> 复刻项目 -> 架构解析 -> 工程对照”的顺序学习：

- 读官方文档，理解 hooks、subagents、MCP、GitHub Actions、permissions。
- 读公开分析论文，抽象出 agent harness 的设计空间。
- 跟随 [learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) 从零复刻核心机制。
- 对照 [hello-agents](https://github.com/datawhalechina/hello-agents)、[OpenClaw](https://github.com/openclaw/openclaw)、[Hermes Agent](https://github.com/NousResearch/hermes-agent) 这些开源项目，学习工程化实现。

| Resource | Focus |
| --- | --- |
| [Claude Code Common Workflows](https://code.claude.com/docs/en/tutorials) | 官方工作流教程，适合学日常使用和项目协作。 |
| [Claude Code Overview](https://code.claude.com/docs/en/overview) | 官方入口，理解产品能力和命令行工作方式。 |
| [learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | 从零复刻 Claude Code-like agent，适合学 harness 最小实现。 |
| [Claude Code 源码解析](https://claudecoding.dev/) | 中文架构解读，适合按模块理解实现思路。 |
| [Claude Code 源码分析地图](https://code.claudecn.com/) | 用地图方式拆解 agent loop、工具、命令和多代理协作。 |
| [Dive into Claude Code](https://arxiv.org/abs/2604.14228) | 从研究视角总结 Claude Code 的设计空间和 agent harness 模式。 |
| [Agentic Education](https://arxiv.org/abs/2604.17460) | 用 Claude Code 学 Claude Code 的交互式课程思路。 |

## Learning Principles

- Build first, then read deeper.
- Prefer small reliable agents over impressive demos.
- Use tools with strict schemas.
- Add evals before you add more agents.
- Trace every important run.
- Treat multi-agent as a coordination problem.
- Keep humans in the loop for risky actions.
- Respect platform rules, copyrights, and data access boundaries.

## Contributing

Good contributions are welcome. Please prefer:

- official docs and official engineering blogs;
- high-quality papers and benchmarks;
- open-source repositories with runnable code;
- serious technical blogs with original insight;
- small projects that help learners practice one specific skill.

Please avoid:

- copied platform posts;
- course ads without substantial content;
- private or paywalled material;
- scraping-oriented content that bypasses platform rules.
