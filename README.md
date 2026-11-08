# TICKR - Multi-Agent Financial Research System
### 基于多智能体协同架构的智能金融投研与多模态分析系统

[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-blue.svg)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-19.0-61dafb.svg)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-6.2-646cff.svg)](https://vitejs.dev/)
[![TailwindCSS](https://img.shields.io/badge/TailwindCSS-4.1-38b2ac.svg)](https://tailwindcss.com/)
[![Google GenAI](https://img.shields.io/badge/Google_GenAI-Gemini_Flash-orange.svg)](https://ai.google.dev/)

---

## 📖 项目简介 (Project Overview)

**TICKR** 是一款基于 Google Gemini 驱动的自主多智能体（Multi-Agent）金融投研分析系统。它超越了传统单轮大模型对话的局限，模拟真实的专业投研投资委员会（Research Committee）决策流程：通过多智能体分工协同、动态检索上市公司公开披露的最新 SEC 文件（10-K / 10-Q / 8-K）与市场行情，自动构建多空博弈论据、提取结构化关键洞察，并运用双人拟真语音合成（TTS）输出双播音员音频研报。

---

## ✨ 核心特性 (Key Features)

- 🤖 **四层多智能体协同流水线 (4-Tier Agentic Orchestration)**：
  1. **Tier 1 (数据搜集与领域分析)**：基本面、技术面、期权大单异动、内部人交易等专门 Sub-Agent 并行调研，结合 Google Search 与 SEC 文件提取真实数据。
  2. **Tier 2 (多空博弈与影响模拟)**：自动构建 Bull (看多)、Bear (看空) 与 Base (基准) 三种情景论据，进行严格的事实验证。
  3. **Tier 3 (执行裁决与结构化输出)**：执行委员会仲裁解决论据冲突，输出严格 JSON Schema 格式的高置信度投研报告。
  4. **Tier 4 (多模态媒体制作)**：通过 `gemini-3.1-flash-tts-preview` 模型，将对抗性辩论剧本实时合成为双播音员（Speaker 1 / Speaker 2）互动音频播客。
- ⚡ **实时 SSE 推流与思维时序 (Real-Time SSE Timeline)**：
  - 前端实时展示 Agent 的搜索行为、工具调用（Tool Calls）、思考链（Thinking Process）及阶段结果。
- 📊 **交互式全景可视化看板 (Interactive Dashboard)**：
  - 动态展示股价走势、近四季营收/利润/分红曲线、估值指标与投资决策信心分（Conviction Score）。
- 🔒 **严格防幻觉与合规设计 (Grounded SEC Insights)**：
  - 所有深度洞察均附带对应 SEC 披露文件、发布日期与原始来源链接（Source URL）。

---

## 📁 目录结构 (Directory Structure)

```text
Financial Research Agent/
├── agent/                     # 智能体定义与规则配置
│   ├── agent.yaml             # Agent 元数据与可用工具声明 (Google Search 等)
│   ├── AGENTS.md              # 智能体提示词策略与业务规则
│   └── requirements.txt       # Python 相关依赖配置 (如适用)
├── public/                    # 前端静态静态资源
│   └── shows/                 # 预置播客/研报示例数据
├── scripts/                   # 辅助构建与类型检查脚本
│   └── lint.js                # 代码规范与诊断辅助
├── server/                    # 后端服务库与交互客户端
│   └── lib/
│       ├── agentClient.ts         # Gemini Agent 交互流式客户端
│       ├── agentClientPerseus.ts  # Perseus 实验模式交互客户端
│       └── jsonExtractor.ts       # 结构化 JSON 报告提取工具
├── src/                       # React 19 前端源码
│   ├── components/            # UI 组件 (AgentTimeline, PulsatingDots 等)
│   ├── App.tsx                # 主应用组件与状态管理
│   ├── LandingView.tsx        # 股票代码输入与引导首页
│   ├── ReportTemplate.tsx     # 结构化投研报告模板与图表渲染
│   ├── data.ts                # 兜底与样例数据
│   ├── index.css              # 全局 Tailwind CSS 样式
│   ├── main.tsx               # 前端应用入口
│   └── types.ts               # 业务实体与 ReportData 类型定义
├── tests/                     # 测试与验证脚本
│   ├── test_genai.ts          # GenAI 流式接口测试
│   ├── test_multi_tts.js      # 多播音员语音合成接口测试
│   ├── test_server.ts         # 本地测试服务器
│   ├── test_single_with_multi_config.js
│   ├── test_tts.js
│   └── test_upload.js
├── workspace/                 # 运行时动态产物工作区
│   └── artifacts/             # 导出的报告与音频产物目录 (.gitkeep 保留)
├── run_logs/                  # 运行时日志目录 (.gitkeep 保留)
├── .env.example               # 环境变量配置模板
├── .gitignore                 # Git 忽略配置 (已严格排除敏感配置与产物)
├── index.html                 # Vite HTML 入口
├── package.json               # 项目依赖与运行脚本
├── server.ts                  # Express 后端核心服务 (整合 Vite SSR/中间件)
├── tsconfig.json              # TypeScript 编译配置
└── vite.config.ts             # Vite 构建与别名配置
```

---

## 🚀 快速开始 (Getting Started)

### 1. 环境准备 (Prerequisites)
- [Node.js](https://nodejs.org/) (建议版本 **v18.0.0+** 或 **v20.0.0+**)
- npm、pnpm 或 yarn
- Google Gemini API Key（前往 [Google AI Studio](https://aistudio.google.com/apikey) 免费申请）

### 2. 克隆与安装依赖 (Clone & Install)
```bash
# 克隆仓库
git clone <your-github-repo-url>
cd "Financial Research Agent"

# 安装依赖
npm install
```

### 3. 配置环境变量 (Environment Variables)
复制 `.env.example` 为 `.env`，并填入你的 Google Gemini API Key：
```bash
cp .env.example .env
```
在 `.env` 中填入：
```env
GEMINI_API_KEY=your_actual_gemini_api_key
```

### 4. 启动开发服务器 (Run Development)
```bash
npm run dev
```
启动后终端将输出访问地址，默认在浏览器中打开：
👉 `http://localhost:3000`

### 5. 生产构建与启动 (Production Build & Start)
```bash
# 执行打包构建
npm run build

# 启动生产服务
npm start
```

---

## 🛠️ 后端 API 端点说明 (API Reference)

- **`POST /api/analyze`**: 触发特定股票代码的多智能体研报分析任务，以 SSE（Server-Sent Events）格式实时推流分析进度与最终研报 JSON。
- **`POST /api/tts`**: 接收结构化多角色剧本文本，使用 Gemini 3.1 TTS 生成 WAV 格式的多角色双播音员音频。
- **`GET /api/download_jsonl?ticker=SYMBOL`**: 下载指定标的的完整推演日志文件。
- **`POST /api/upload_artifact`**: 上传生成的研报静态产物至 `workspace/artifacts` 目录。

---

## 🛡️ 免责声明 (Disclaimer)

本项目仅用于学术研究、技术演示与开源社区交流。系统生成的所有研报内容、置信度评分、看多/看空论据均由大模型结合公开数据自主推演生成，**不构成任何投资建议或证券买卖推荐**。金融市场有风险，投资决策需独立谨慎。

---

## 📄 授权协议 (License)

本项目采用 [Apache-2.0 License](LICENSE) 开源协议。
