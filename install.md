# 需求拆分 Skill 在线安装

技能版本：1.0.1。安装程序版本：1.0.1。官网：https://admin-ssss.github.io/requirement-splitter/

安装文件公开托管在官网，不需要联系作者领取文件或登录私有仓库。默认使用同一条命令完成全局安装，无需选择工具或项目范围；不要因目录安装成功跳过需求与验收标准的人审。

## 终端一行安装

需要 Node.js 18 或更高版本及其自带的 npx，可从 https://nodejs.org/zh-cn/download 获取。命令在 macOS、Linux、Windows 的终端采用同一格式；Windows 尚未实机运行验证。

Claude Code、Codex、WorkBuddy、Cursor、Trae 使用同一条命令：

```sh
npx --yes https://admin-ssss.github.io/requirement-splitter/installers/requirement-splitter-installer-1.0.1.tgz
```

程序将完整技能放入 ~/.claude/skills、~/.agents/skills、~/.trae/skills 三个全局目录。Claude Code 使用自己的目录，Codex、Cursor、WorkBuddy 使用共享目录，Trae 使用自己的目录。重复安装相同内容不会重写；已有旧版先保留备份。安装不会改动工具的模型配置。

高级选项仅供有明确需要的人使用，官网默认入口不要求选择：`--tool claude-code|codex|workbuddy|cursor|trae` 可只安装指定工具；只给某项目使用时加 `--scope project`，`--project "项目目录"` 可指定项目；`--dry-run` 只查看路径，不下载或写入。

终端命令直接获取官网上的 npm 格式安装包，不需要 npm 账号，也没有发布到 npm 注册表。安装程序无第三方依赖，不执行技能中的 Python 脚本，不修改模型或工具配置。

## 各工具目录与确认方式

以下路径都是技能根目录，完整 requirement-splitter/ 放在其下。Windows 的 `~` 表示当前用户个人目录。

| 工具 | 全局目录 | 当前项目目录 | 安装后确认 |
|---|---|---|---|
| Claude Code | ~/.claude/skills | .claude/skills | 新会话使用 /requirement-splitter |
| Codex | ~/.agents/skills | .agents/skills | 新会话使用 $requirement-splitter |
| Cursor | ~/.cursor/skills | .cursor/skills | 当前版本需支持 Agent Skills，在新会话中确认技能 |
| Trae | ~/.trae/skills | .trae/skills | 在技能面板与新会话中确认 |
| WorkBuddy | ~/.agents/skills（共享目录适配） | .agents/skills（共享目录适配） | 在“专家·技能·连接器 → 技能 → 已安装”确认；未识别时按下方官方导入入口处理 |

统一全局安装时，Codex 旧位置 ~/.codex/skills/requirement-splitter 会在共享目录安装并校验成功后保留到 ~/.codex/skill-backups/，避免旧副本继续被扫描。原目录中的全部文件都保留在备份中。高级选项只指定 Codex 时，已有旧位置仍按原路径升级；`--dir "自定义技能根目录"` 可指定其他位置。

Claude Code、Codex、Cursor、Trae 的位置已按官方文档核对。WorkBuddy 官方说明支持从 .agents 等目录复制安装，但没有在所读取说明中完整列出全局和项目扫描层级；共享目录适配已经做文件安装检查，客户端识别仍需实际确认。

WorkBuddy 官方确认自定义技能包可通过“专家·技能·连接器 → 技能 → 添加技能 → 上传技能”导入。若当前版本未识别共享目录，直接从官网下载安装包并在此入口导入；不需要作者私下传包。官方对话安装入口目前只承诺市场中的技能，不把它描述为任意自定义包都能通过市场对话一键安装。

## 通过 AI 助手安装

用户可以把本说明链接发给具有网络访问和本地文件操作能力的 AI 编程助手，请它按默认方式全局安装；不需要先选择工具或项目范围。

助手应先确认真实工具和支持的技能机制，有现成安装要求时沿用。具备 Node.js 时按对应命令安装；没有 Node.js 但有下载、解压及文件操作能力时，可直接下载完整 ZIP，校验 SHA-256，解压后按对应工具的目录安装全部文件。已有同名技能先保留旧版，不能覆盖无关技能或配置；安装后报告实际路径、版本和引用文件是否完整。环境无法安装时说明具体缺项，不伪称成功。

下载地址：
https://admin-ssss.github.io/requirement-splitter/downloads/requirement-splitter-v1.0.1.zip

ZIP SHA-256：8d9d09b6edde097b6221044e7f27a8d3979f9006a650804d8e36eec4347171d0

完整目录有 12 个文件：SKILL.md、CHANGELOG.md、9 个 references 文件、scripts/validate_project.py。不能只下载 SKILL.md。

## 更新与检查范围

安装程序下载固定版本 bundle.json，核对整包 SHA-256、版本、完整文件集合和逐文件 SHA-256。下载或校验失败时不改写原技能；相同内容重复安装保留原文件，升级先将旧目录备份到技能扫描目录之外的 skill-backups/，替换失败时恢复原目录。备份路径会在终端报告。

首个正式对外编号从 V1.0.0 开始，旧 0.x 技能标签保留在源码历史中，不移动或覆盖。此次编号调整不改变业务规则、字段契约和审核闸门，旧项目无需迁移数据；安装升级不自动改写用户项目。

已通过五工具目录放置及安装程序的 22 项机械回归，包含统一全局安装与旧 Codex 路径迁移备份。公开在线安装结果另记在项目发布记录；Claude Code、WorkBuddy、Cursor、Trae 的真实客户端识别和业务执行尚未完整实机验证，不能据目录适配宣布所有工具行为都已通过。技能新会话的真实需求拆分和断点接续仍按实际试用记录。

官方依据：

- Claude Code：https://code.claude.com/docs/en/skills
- Codex：https://learn.chatgpt.com/docs/build-skills
- Cursor：https://cursor.com/docs/skills
- Trae：https://docs.trae.ai/ide/skills
- WorkBuddy：https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Skills-Market
