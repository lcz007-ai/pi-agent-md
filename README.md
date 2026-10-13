# pi-agent-md

一组用于 Pi 的个人级和项目级指令范本，帮助把长期协作偏好、机器环境事实与项目约定分层管理。文件是配置/示例材料；放在仓库根目录并不会自动成为你的个人全局配置。

## 文件

- [`AGENTS.md`](AGENTS.md)：本机最新的全局协作规范范本，适合放入 Pi agent 目录。
- [`APPEND_SYSTEM.md`](APPEND_SYSTEM.md)：个人记忆和规则范本，由 Pi 追加到默认 system prompt；其中含有个性化配置,建议按具体条件二次配置(系统环境、技能、插件等)。
- [`项目AGENTS模板.md`](项目AGENTS模板.md)：项目级模板。复制到项目根目录并命名为 `AGENTS.md`，只填写该项目特有、助手不易推断且经常需要的事实。



## 具体使用
 
### 1.配置全局(必须)
```text
AGENTS.md          → <agent-dir>/AGENTS.md
```
把文件复制到 Pi 的 agent 目录（默认 `~/.pi/agent`）

### 2.配置记忆(可选)
```text
APPEND_SYSTEM.md   → <agent-dir>/APPEND_SYSTEM.md
``` 
按需取用:
- 注意把`(for mac)`这些后缀去掉
- 对个人模型、环境和插件工具的约定,按需调整。
- 不要将 API key、token 等明文凭证放入其中.
   
### 3.项目规则(可选)
```text
APPEND_SYSTEM.md   → <project-dir>/AGENTS.md
```
按需取用:
- 手动复制 [`项目AGENTS模板.md`](项目AGENTS模板.md) 到目标项目根目录并重命名为 `AGENTS.md`,**再让AI填写具体内容**.
- 填入该项目的技术栈、命令、约束和已知坑。项目级 system prompt 或设置放在项目 `.pi/` 目录，并注意项目信任提示。
 



## 如何个性化

- **对话风格与工作规则**：修改个人 `<agent-dir>/AGENTS.md`；项目特定事实写在项目根目录 `AGENTS.md`。
- **默认system prompt**：通常用 `<agent-dir>/APPEND_SYSTEM.md` 追加少量稳定规则；只有确需完全接管默认提示时才用 `SYSTEM.md`。
- **运行偏好**：用 `<agent-dir>/settings.json` 设置默认模型、thinking、工具、会话、界面等；项目 `.pi/settings.json` 可覆盖/补充项目设置。
- **快捷键与界面**：`keybindings.json` 自定义按键，主题 JSON 自定义颜色。
- **可复用能力**：skills 提供按需加载的专项指引；prompt templates 提供可调用的提示模板；extensions 增加工具、命令、事件处理或界面功能。

建议先用指令文件和设置解决问题；需要可执行行为时再考虑 extension。Extension 在 Pi 进程内运行，权限与 Pi 相同；安装或信任第三方项目资源前应先审查。


# 附录
 
## Pi 如何加载指令

Pi 从启动时的工作目录确定项目范围，并组合 system prompt、对话历史、工具和已发现的上下文资源。可把指令分成两类理解：

1. **上下文文件**：agent 目录、当前工作目录及其父目录中的 `AGENTS.md`、`AGENTS.MD`、`CLAUDE.md` 等会作为适用目录的项目/全局说明加载。`AGENTS.override.md` 只替代同目录的 `AGENTS.md` 或 `CLAUDE.md`，不影响其他目录的上下文文件。
2. **系统提示文件**：`<agent-dir>/APPEND_SYSTEM.md` 为 Pi 默认 system prompt 追加内容；`<agent-dir>/SYSTEM.md` 则整体替换默认 system prompt。项目级对应文件放在 `.pi/APPEND_SYSTEM.md` 或 `.pi/SYSTEM.md`。获信任后，项目级同名系统提示文件优先于个人 agent 目录中的文件，**不是与个人文件合并**。

默认 agent 目录是 `~/.pi/agent`，可由 `PI_CODING_AGENT_DIR` 更改。Windows 默认通常对应 `%USERPROFILE%\.pi\agent`。因此，本仓库中的 `APPEND_SYSTEM.md` 需要复制到该目录后才作为个人追加规则生效；只放在仓库根目录不会自动加载。

项目 `.pi/settings.json` 及 `.pi/extensions`、`.pi/skills`、`.pi/prompts`、`.pi/themes` 等项目资源受项目信任控制。`AGENTS.md` 等上下文文件仍可能在未信任项目时加载；把项目设为可信也不等于沙箱，工具和扩展仍受 Pi 进程本身的操作系统权限约束。对陌生项目、指令和扩展应先检查。

修改活动会话中的指令、设置或资源后，可运行 `/reload` 重新加载。Pi 的启动摘要可显示本次加载的上下文和资源。

## Pi 官方文档

- [配置与文件位置](https://github.com/earendil-works/pi/blob/main/docs/configuration.md)
- [上下文与使用方式](https://github.com/earendil-works/pi/blob/main/docs/usage.md)
- [项目资源信任与安全](https://github.com/earendil-works/pi/blob/main/docs/security.md)
- [设置](https://github.com/earendil-works/pi/blob/main/docs/settings.md)
- [Skills](https://github.com/earendil-works/pi/blob/main/docs/skills.md)、[Prompt templates](https://github.com/earendil-works/pi/blob/main/docs/prompt-templates.md)、[Extensions](https://github.com/earendil-works/pi/blob/main/docs/extensions.md)、[Themes](https://github.com/earendil-works/pi/blob/main/docs/themes.md)
