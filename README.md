# CodeLab · 多语言代码实验室

一个集成网站:自动检测本机已安装的编程语言环境,在网页里写代码、点一下就运行;
没装的语言直接给出安装命令,照着装完点"刷新检测"即可。内置 **AI Agent 中心**
(主流 AI 编程 Agent 的下载与部署指引)。

- **线上版(关机可用)**: https://hayden-h-cmyht.github.io/code-lab/
  网页预览 / JS / TS / Python(Pyodide)可直接跑;全部语言需本地版
- **本地完整版**: 双击桌面 `CodeLab`(或项目里的 `start.bat`)

## 三大板块

1. **多语言运行**:15 种语言环境检测 + 代码运行
   (Python / JavaScript / TypeScript / C / C++ / Java / Go / Rust / PHP / Ruby /
   Lua / Bash / PowerShell / Perl / R / 网页预览)
2. **环境部署**:未安装的语言给 winget 一键安装命令,装完刷新即生效
3. **AI Agent 中心**:Claude Code / Codex CLI / Gemini CLI / OpenCode /
   Qwen Code / Kimi Code CLI / Aider / Cline / Copilot / Cursor /
   通义灵码 / Trae / CodeGeeX / 文心快码 / CodeBuddy / 华为云码道 CodeArts /
   Windsurf / Roo Code / Continue / Ollama / LM Studio / LangGraph / CrewAI /
   Dify / n8n / 扣子 Coze —— 安装命令一键复制 + 三步部署指引(2026-08 现状);
   支持 **⚡ 一键自动安装**(`install_agents.ps1`, 自动补装环境 + 批量安装 + 校验)
   与 **📖 安装教程**(网页弹窗 + `INSTALL_TUTORIAL.md`)

## 桌面启动端

`C:\Users\86138\Desktop\CodeLab.lnk`(带 Python 图标)与 `CodeLab.bat`:
双击启动本地引擎并自动打开浏览器;**引擎已在运行时再双击只会新开一个浏览器
标签**,不会重复起服务。

## 功能

- **环境自动检测**:进入页面即扫描本机所有语言及版本,侧栏绿点=可用
- **代码运行**:编译型语言自动编译+运行,显示编译错误;支持标准输入(stdin)、
  运行超时保护(超时杀整个进程树)、输出截断保护
- **编辑器**:语法高亮、行号、Tab/Shift+Tab 缩进、自动缩进、Ctrl+Enter 运行、
  每种语言的草稿自动保存(localStorage)
- **网页预览**:HTML/CSS/JS 三件套 iframe 实时预览
- **AI Agent 一键自动安装**:Agent 面板点「⚡ 自动安装」复制一条命令, 或在项目目录运行
  `powershell -ExecutionPolicy Bypass -File .\install_agents.ps1` —— 自动检查并补装
  Node/Python/winget/VSCode, 选分类勾编号批量安装, 装完自动校验(npm / pip / winget /
  VSCode 扩展); 支持 `-List` / `-Agents kimi,cursor` / `-All`
- **AI Agent 安装教程**:Agent 面板点「📖 教程」弹出图文教程(环境检查 → 自动安装 →
  手动安装 → 登录/配 Key → 常见问题), 完整版见 `INSTALL_TUTORIAL.md`
- **双形态自适应**:有本地引擎跑全部语言;没有引擎(线上/直接开 html)时
  JS / TS / Python(WASM)/ 网页预览照常可用

## 启动

```
桌面: 双击 CodeLab
项目: 双击 start.bat
```

依赖:本机装有 Python 3.10+(仅用于跑本地服务器;检测/运行其他语言不依赖它)。

## API(本地引擎,127.0.0.1:8790 起)

- `GET  /api/env` — 环境检测;`?refresh=1` 强制重新扫描
- `GET  /install_agents.ps1` — 自动安装脚本(供「⚡ 自动安装」一键命令下载)
- `GET  /install_tutorial.md` — 安装教程文档(可下载)
- `POST /api/run` — body: `{lang, code, stdin, timeout(秒)}`
  返回 `{ok, stdout, stderr, exit_code, compile_error, timed_out, duration_ms}`

安全边界:服务器只监听 127.0.0.1;代码在本机临时目录执行,用完即删;
默认超时 10 秒。它就是"在本机跑代码",请勿把端口暴露到公网。

## 文件

```
C:\Users\86138\Desktop\CodeLab.lnk/.bat   桌面启动端
start.bat                                 项目内启动脚本
server.py                                 本地引擎(环境检测 + 运行 API + 脚本/教程下载)
index.html                                前端单文件(本地/线上自适应 + Agent 中心)
install_agents.ps1                        AI Agent 一键自动安装脚本(⚡ 自动安装)
INSTALL_TUTORIAL.md                       AI Agent 安装教程(📖 教程, 完整版)
_deploy_online.py                         部署线上版(gh api Contents API,绕 git push)
gui-test-screenshots/                     GUI 测试证据截图
```

## 更新线上版

```
py _deploy_online.py
```
