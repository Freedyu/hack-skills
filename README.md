# HACKING SKILLS / HackSkills

面向 **漏洞赏金、Web 安全、API 安全、授权渗透测试场景** 的 Agent Skills 知识库。

这个仓库的目标很直接：把高质量、可审查、适合 Agent 加载的安全技巧整理成一套 **HackSkills**，让用户和 AI 在真实场景里更稳定地完成复杂安全任务。

## 为什么使用这个仓库

- **安全优先**：本仓库非常重视供应链与内容安全，所有 PR 都应经过认真审核，并持续评估是否存在投毒风险。
- **知识库优先**：内容以知识库和方法论为主，补足 AI 常见盲区，放大 Agent 在安全领域的实战能力。
- **欢迎 PR**：我们非常欢迎贡献新的技巧、案例、方法论和修订，PR 是扩展本仓库知识边界的最好方式。

## 当前提供的能力

- Recon / Methodology
- XSS / SQLi / SSRF / XXE / SSTI
- IDOR / BOLA / BFLA
- CSRF / JWT / OAuth / Auth Bypass
- Path Traversal / LFI / Command Injection / NoSQL Injection
- API Security / Business Logic

完整索引见：

- `skills/BUGBOUNTY_SKILLS.md`

## 安装方式

本仓库现在提供了一个兼容 **SKILL.md / Agent Skills** 常见规范的安装入口：

- **skill id**: `hackskills-bugbounty-hunter`
- **raw URL**: `https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hackskills-bugbounty-hunter/SKILL.md`

如果你的命令行工具支持通过 **GitHub raw URL** 或 **SKILL.md 文件** 安装技能，可以直接使用上面的入口。

### 1) Claude Code

项目内安装：

```bash
mkdir -p .claude/skills && \
curl -fsSL https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hackskills-bugbounty-hunter/SKILL.md \
  -o .claude/skills/hackskills-bugbounty-hunter.md
```

全局安装：

```bash
mkdir -p ~/.claude/skills && \
curl -fsSL https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hackskills-bugbounty-hunter/SKILL.md \
  -o ~/.claude/skills/hackskills-bugbounty-hunter.md
```

### 2) OpenAI Codex / Codex CLI

```bash
mkdir -p .codex/skills && \
curl -fsSL https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hackskills-bugbounty-hunter/SKILL.md \
  -o .codex/skills/hackskills-bugbounty-hunter.md
```

### 3) Gemini CLI

```bash
mkdir -p .gemini/skills && \
curl -fsSL https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hackskills-bugbounty-hunter/SKILL.md \
  -o .gemini/skills/hackskills-bugbounty-hunter.md
```

### 4) Cursor

```bash
mkdir -p .cursor/skills && \
curl -fsSL https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hackskills-bugbounty-hunter/SKILL.md \
  -o .cursor/skills/hackskills-bugbounty-hunter.md
```

### 5) 作为完整知识库仓库使用

如果你希望保留完整索引和全部专题文档，建议直接克隆仓库：

```bash
git clone https://github.com/yaklang/hack-skills.git
cd hack-skills
```

然后优先阅读：

- `skills/BUGBOUNTY_SKILLS.md`
- `skills/Recon_and_Methodology.skill.md`

## 推荐使用方式

### 场景 A：你想一键装进常见 Agent 工具

优先安装：

- `hackskills-bugbounty-hunter`

这个入口适合：

- Claude Code
- Codex / Codex CLI
- Gemini CLI
- Cursor
- 其他兼容 `SKILL.md` 的工具

### 场景 B：你要做长期漏洞赏金 / 安全研究

直接使用整个仓库，因为这里的价值不仅在单一 skill，还在于：

- 主索引会告诉 Agent 先加载哪一类技能
- 各专题文件保留了更完整的攻击路径、枚举思路与经验细节
- 更适合把仓库当作安全知识库长期维护

## 检索关键词

如果你的安装器、索引器、技能市场或内部平台支持名称/标签检索，建议使用这些关键词：

- `HackSkills`
- `HACKING SKILLS`
- `bug bounty`
- `bugbounty`
- `bug bounty hunter`
- `赏金猎人`
- `web security`
- `api security`

## 仓库结构

```text
hack-skills/
├── README.md
└── skills/
    ├── BUGBOUNTY_SKILLS.md
    ├── hackskills-bugbounty-hunter/
    │   └── SKILL.md
    ├── Recon_and_Methodology.skill.md
    ├── XSS_Cross_Site_Scripting.skill.md
    ├── SQLi_SQL_Injection.skill.md
    ├── SSRF_Server_Side_Request_Forgery.skill.md
    └── ...
```

## 信任与安全声明

- 本仓库把 **内容可审查性** 放在第一位。
- 我们默认把 PR 审核视为安全边界的一部分。
- 我们会持续关注恶意投毒、误导性技巧、危险默认建议等风险。
- 所有内容都应以 **授权测试、合法研究、最小化风险** 为前提使用。

## 贡献方式

欢迎提交 PR 来扩展：

- 新漏洞类别
- 更好的漏洞赏金方法论
- Agent 更容易忽略的边界条件
- 更高质量的结构化知识整理
- 错误修正、去噪、风险提示、术语统一

如果你准备贡献内容，建议优先保证：

- 可验证
- 可审查
- 不鼓励未授权攻击
- 能帮助 Agent 在真实任务中更稳健地推理和执行
