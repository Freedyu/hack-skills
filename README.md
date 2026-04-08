# HACKING SKILLS / HackSkills

面向漏洞赏金、Web 安全、API 安全与授权测试场景的 Agent Skills 知识库。

这个仓库的目标很明确：把高质量、可审查、适合被 Agent 加载的安全知识整理成一套可安装、可检索、可组合使用的 HackSkills。

## 快速开始

首选安装入口是 `hack`：

```bash
npx skills add yaklang/hack-skills
```

如果你的工具支持直接安装单个 SKILL.md，也可以使用：

- skill id: `hack`
- raw URL: `https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hack/SKILL.md`

安装后，优先从总入口开始，再按漏洞类型加载专题技能。

## 怎么使用

推荐顺序：

1. 先加载 `hack`，让 Agent 判断当前目标属于 Recon、API、授权、认证、注入还是业务逻辑问题。
2. 再根据目标现象进入对应专题目录。
3. 最后回到总索引补足遗漏的链路与组合打法。

适合的使用场景：

- 新漏洞赏金目标的初始测试路线规划
- Web/API 安全测试中的专题技能补全
- 授权边界、认证边界、输入边界的系统化审视
- 把零散现象快速路由到正确漏洞类别

## 仓库结构

```text
hack-skills/
├── README.md
└── skills/
    ├── BUGBOUNTY_SKILLS.md
    ├── hack/
    │   └── SKILL.md
    ├── recon-sec/
    ├── injection-sec/
    ├── auth-sec/
    ├── authz-sec/
    ├── api-sec/
    ├── file-access-sec/
    └── business-logic-sec/
```

目录说明：

- `hack/`: 总入口技能，适合先装先用。
- `recon-sec/`: 信息收集、方法论、目标理解。
- `injection-sec/`: XSS、SQLi、SSRF、XXE、SSTI、CMDi、NoSQL 注入。
- `auth-sec/`: 认证、会话、JWT、OAuth、CSRF。
- `authz-sec/`: IDOR、BOLA、BFLA 等授权问题。
- `api-sec/`: API 安全专项。
- `file-access-sec/`: 路径穿越、LFI、文件访问控制问题。
- `business-logic-sec/`: 竞态、价格篡改、流程绕过等业务逻辑问题。

完整索引见 `skills/BUGBOUNTY_SKILLS.md`。

## 技能选择建议

如果你看到这些现象，优先加载这些目录中的技能：

- HTML/JS 反射与模板表达式：`injection-sec`
- 登录、重置密码、2FA、JWT、OAuth、CSRF：`auth-sec`
- 对象 ID、租户隔离、权限边界：`authz-sec`
- REST API、GraphQL、移动端后端：`api-sec`
- 文件路径、下载接口、上传链路：`file-access-sec`
- 优惠券、库存、支付、流程状态机：`business-logic-sec`
- 新目标、未知攻击面：先从 `recon-sec` 开始

## 安装方式

### 通用安装

```bash
npx skills add yaklang/hack-skills
```

### Raw URL 安装

适用于支持拉取单文件技能的工具：

```bash
curl -fsSL https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hack/SKILL.md
```

### 本地作为知识库使用

```bash
git clone https://github.com/yaklang/hack-skills.git
cd hack-skills
```

建议先读：

- `skills/hack/SKILL.md`
- `skills/BUGBOUNTY_SKILLS.md`
- `skills/recon-sec/Recon_and_Methodology.skill.md`

## 设计原则

- 安全知识优先于花哨包装。
- 内容可审查性优先于数量扩张。
- 优先服务授权测试、合法研究与防御验证场景。
- 目录名带 `-sec`，用于明确这是安全知识分类，不是通用工程目录。

## 贡献方式

欢迎提交 PR，重点方向包括：

- 新漏洞类别与高价值案例
- 更好的漏洞赏金方法论
- Agent 容易忽略的边界条件
- 风险提示、术语统一与内容去噪

贡献内容建议满足：

- 可验证
- 可审查
- 不鼓励未授权攻击
- 能帮助 Agent 在真实任务中更稳健地推理与执行
