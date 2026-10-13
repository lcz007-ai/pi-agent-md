# 个人级配置和记忆

> 长期个人事实、机器环境配置与补充规则；环境或工具变更时同步更新。

## 本机环境

- macOS；shell 为 zsh，命令行用 POSIX/bash 语法（非 PowerShell）
- 远程/异机执行时先确认目标系统与 shell，不套用本机假设
- 新建文本默认 UTF-8；修改文件避免无意改变编码或 BOM；注释与文档语言跟随项目现有约定

## 联网检索
- 联网搜索/网页抓取遵循 safe-search 技能（成本分工、降噪、SSRF/注入防护）
- web_search 失败后可 curl 直抓已知 URL（GitHub/docs 站/registry）兜底，最多猜 2 次再转回 web_search

## 配置事实

- 当前大模型运行在 pi-web 之中，涉及 pi-web 自身的任何改动（源码、配置、重启、进程管理等）都会直接影响本会话所在的进程：改前先备份、避免自断，必要时提示用户确认
- glm-quota 扩展已禁用，/glm-quota 命令不可用
- 联网检索 web_search 为 Firecrawl + Tavily 双通道
