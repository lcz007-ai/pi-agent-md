# 个人级配置与补充规则（memory）

> 长期个人事实、机器环境配置与补充规则；环境或工具变更时同步更新。

## 本机环境
- macOS；shell 为 zsh，命令行用 POSIX/bash 语法（非 PowerShell）
- 远程/异机执行时先确认目标系统与 shell，不套用本机假设
- 新建文本默认 UTF-8；修改文件避免无意改变编码或 BOM；注释与文档语言跟随项目现有约定

## 联网检索
- 流程与安全细节遵循 safe-search-curl 技能；搜索词只含必要公开信息，不带凭证或私有数据

## 交付物与报告
- 生成报告/归档文档时，除给出路径外，必须附可直接点击打开的 file:// 链接（markdown 格式，如 `[报告名](file:///Users/f007/Documents/报告.md)`，路径用绝对路径并 URL 编码特殊字符）

## 配置事实
- 当前大模型运行在 pi-web 之中，涉及 pi-web 自身的任何改动（源码、配置、重启、进程管理等）都会直接影响本会话所在的进程：改前先备份、避免自断，必要时提示用户确认
- glm-quota 扩展已禁用，/glm-quota 命令不可用
- 联网检索 web_search 为 Firecrawl + Tavily 双通道

## pi-web 网关架构（2026-10-12 起）
- pi-web 由常驻微型网关 `~/.local/bin/pi-web-gateway`（launchd: com.f007.pi-web-gateway，:30141）按需拉起/停止，后端固定 30142；设计与运维见 `~/Documents/pi-web-按需启动改造说明.md`
- 一次性运维脚本严禁以 keepalive 注册 launchd 任务（曾致 89 轮无限重启、模型不回复，事故报告：`~/Documents/pi-web-模型不回复事故诊断与修复-20261012.md`）
