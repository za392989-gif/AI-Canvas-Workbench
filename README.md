<img width="2077" height="202" alt="22" src="https://github.com/user-attachments/assets/a504f201-4c6c-441d-9781-f48d8e2eecb4" />



# AI 无限画布工作台
AI Canvas Workbench 是一个纯原生本地优先的 AI 画布工作台。它把无限画布、节点式创作、AI 生图/编辑、本地模型、本地项目管理和 Electron 桌面壳整合在一起，目标是做一个可离线管理资产、可接入多种 AI API、也能调用本地模型的创作工具。

## 技术架构
项目采用三层结构：
原生 Web 前端
  index.html / main.js / src / styles / api

Python 本地后端
  server.py / backend/services

Electron 桌面壳
  electron/main.js / electron/preload.cjs

前端负责画布、节点、面板、交互和任务状态展示；Python 后端负责本地 API、项目文件、上传资产、裁剪/蒙版/诊断包、AI 任务队列和本地模型调用；Electron 桌面启动、本地后端拉起、系统剪贴板、本地保存、便携数据目录和打包发布。

## 核心功能 
无限画布：节点拖拽、缩放、多画布页、资源节点、生成节点、历史节点。
AI 生成：支持多服务商配置，包括 RunningHub、GRSAI、ToAPIs、OpenAI/Gemini 兼容接口、自定义 API。
任务队列：AI 请求提交后返回 taskId，前端通过任务中心统一查询状态。
本地模型：支持本地抠图模型，例如 rembg ONNX、BiRefNet；用户模型优先读取便携数据目录，内置模型作为兜底。
图片工具：上传、标注、蒙版、重绘、擦除、裁剪、宫格裁剪、派生输出。
项目管理：本地保存、加载、导入导出 .aicanvas 项目包。
自动编号保存：保存/导出/下载使用日期编号，避免覆盖旧文件。
诊断包：可收集日志、配置摘要、运行信息，并对 API key/token 做脱敏。
桌面便携版：不依赖系统安装 Python，双击 exe 即可启动。

## 便携数据目录
Electron 发布版采用“程序和用户数据分离”的结构：
AI-Canvas-Workbench-Electron/
  AI-Canvas-Workbench-Electron.exe
  runtime/
  AI-Canvas-Workbench-Data/
runtime 只放 Electron、Python 后端和依赖。
AI-Canvas-Workbench-Data 放用户数据，包括：
config.json        API 配置和应用配置
security.json      本地 API token
projects/          项目保存文件
assets/            上传素材
output/            生成、裁剪、蒙版等输出
exports/           用户主动导出/下载的文件
models/            用户导入的本地模型
logs/              运行日志
app-state/         画布快照、缓存、偏好
workflows/         工作流文件
temp/              临时文件
迁移时只需要移动整个 AI-Canvas-Workbench-Electron 文件夹；清空个人数据时删除 AI-Canvas-Workbench-Data 即可。
## Windows系统  一键整合包 解压即用（推荐普通用户）
1.下载整合包
2.解压文件 将下载的压缩包解压到不带中文的路径，
一键启动 AI-Canvas-Workbench-Electron.exe
