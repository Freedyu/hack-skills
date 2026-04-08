# HACK.SKILLS - Hacker Arsenal for Agents

<p align="right">English | <a href="./README_CN.md">中文</a></p>

<p align="center">
    <img src="./assets/readme-hero-banner.jpg" alt="HackSkills Hero Banner" width="100%" />
</p>

<p align="center">
    <strong>Master Entry → Category Entries → Deep Topic Skills</strong><br/>
    One master entry, six stable category entries, and a set of flat security topic skills drilled down on demand.
</p>

An Agent Skills knowledge base for bug bounty, web security, API security, and authorized testing.

The current branch has converged to a standard directory structure: every skill lives in its own directory, uniformly using `skills/{semantic-identifier}/SKILL.md`. The design goal is not to expose every minor tip as an entry point, but to compress what the loader truly needs to see into one master entry, six category entries, and deep topic skills drilled down on demand.

The objective is straightforward: organize security knowledge that is genuinely useful in real engagements and easy to audit and maintain into a set of installable, searchable, and composable HackSkills.

## Knowledge Sources & Distillation Boundaries

This repository is not a mirror of external materials — it is a distillation layer aimed at Agents.

Current primary reference sources:

- `gh0stkey/Web-Fuzzing-Box`: Provides scenario-organized dictionaries, payloads, and fuzzing components, suitable for distilling into taxonomies and small-sample selection strategies.
- `BugBountyBooks`: Provides bug bounty methodologies, testing routines, and topic drafts suitable for skill-based organization.
- `swisskyrepo/PayloadsAllTheThings`: Provides high-value payload families, bypass techniques, and exploit chain directions, suitable for distilling into scenario-based indices and method matrices.

Processing principles for these sources:

- No direct copying of large dictionaries or full payload lists.
- Prioritize distilling into routable, composable, and auditable security skills.
- Use small, stable samples, taxonomies, and cross-references to improve Agent stability in real security scenarios.

## Quick Start

The preferred entry point is `hack`:

```bash
npx skills add yaklang/hack-skills
```

If your tooling supports pulling a single SKILL.md directly, you can also use:

- frontmatter name: `hack`
- raw URL: `https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hack/SKILL.md`

After installing, the recommended order is simple: start from the master entry, then move into category entries, and only then drill into deep topic skills.

## Loader Priority

To better match real-world loader usage, this repository organizes skills into three layers.

After the latest round of adjustments, the entry layer uniformly follows two constraints:

- `directory name = frontmatter name`, to avoid directory consistency errors from the skill validator.
- descriptions use the more concise `Entry P0 / Entry P1` template, making entry levels easier to understand for both loaders and human readers.

| Layer | Role | Recommended Exposure | Representative Skill |
|---|---|---|---|
| Master Entry | Global routing, test sequencing, cross-category switching | Expose first | [hack](./skills/hack/SKILL.md) |
| Category Entry | Route by attack surface to stable topic families | Expose first | [recon-for-sec](./skills/recon-for-sec/SKILL.md), [api-sec](./skills/api-sec/SKILL.md), [auth-sec](./skills/auth-sec/SKILL.md) |
| Deep Topic | Provide complete attack playbooks and execution details | Load on demand | [xss-cross-site-scripting](./skills/xss-cross-site-scripting/SKILL.md), [jwt-oauth-token-attacks](./skills/jwt-oauth-token-attacks/SKILL.md) |

Short skills like payload-selection, default credentials, username generation, and port focus have now been merged back into their main topics or category entries. Loaders only need to prioritize these three layers and no longer need to deal with mid-tier fragment skills.

## How to Use

Recommended order:

1. Load `hack` first and let the Agent determine whether the current task looks more like recon, API, authentication/authorization, injection checking, file access, or business logic.
2. Then enter the corresponding category skill, rather than jumping straight to a very specific topic.
3. Only enter a deep topic skill when the symptom is already clear.
4. Payload selection, small dictionaries, and quick sample selection are handled directly within the corresponding main topic — no need to jump to a separate helper entry.

Best suited for these scenarios:

- Just received a new target and need to determine the test route first.
- In a web/API security test and want to fill in topic-specific methods.
- Need to systematically cover authentication, authorization, input boundaries, and business boundaries.
- Have only scattered observations and want to quickly route to the correct vulnerability category.

## Main Entry Points

| Type | Skill | Purpose | When to Use First |
|---|---|---|---|
| Master Entry | [hack](./skills/hack/SKILL.md) | Global routing, phase assessment, cross-category switching | New target, unknown attack surface, want to establish methodology first |
| Category Entry | [recon-for-sec](./skills/recon-for-sec/SKILL.md) | Asset discovery, technology identification, test starting points | Just received the target, insufficient information |
| Category Entry | [api-sec](./skills/api-sec/SKILL.md) | REST, GraphQL, mobile backend routing | Observed API interfaces or OpenAPI |
| Category Entry | [auth-sec](./skills/auth-sec/SKILL.md) | Authentication, sessions, OAuth, JWT, object authorization | Observed login, tokens, object IDs, cross-tenant |
| Category Entry | [injection-checking](./skills/injection-checking/SKILL.md) | XSS, SQLi, SSRF, XXE, SSTI, CMDi, NoSQL routing | Input enters an interpreter or execution environment |
| Category Entry | [file-access-vuln](./skills/file-access-vuln/SKILL.md) | Upload, download, LFI, path control, processing chains | File names, paths, downloads, previews, uploads |
| Category Entry | [business-logic-vuln](./skills/business-logic-vuln/SKILL.md) | Race conditions, pricing, workflow, state machine issues | Coupons, inventory, payments, approvals, quotas |

Current frontmatter names in the entry layer match directory names one-to-one: `hack`, `recon-for-sec`, `api-sec`, `auth-sec`, `injection-checking`, `file-access-vuln`, `business-logic-vuln`.

## Category to Topic Mapping

| Category | Recommended First Read | Common Drill-Down Topics |
|---|---|---|
| Recon | [recon-for-sec](./skills/recon-for-sec/SKILL.md) | [recon-and-methodology](./skills/recon-and-methodology/SKILL.md) |
| API | [api-sec](./skills/api-sec/SKILL.md) | [api-recon-and-docs](./skills/api-recon-and-docs/SKILL.md), [api-authorization-and-bola](./skills/api-authorization-and-bola/SKILL.md), [api-auth-and-jwt-abuse](./skills/api-auth-and-jwt-abuse/SKILL.md) |
| Auth | [auth-sec](./skills/auth-sec/SKILL.md) | [authbypass-authentication-flaws](./skills/authbypass-authentication-flaws/SKILL.md), [jwt-oauth-token-attacks](./skills/jwt-oauth-token-attacks/SKILL.md), [idor-broken-object-authorization](./skills/idor-broken-object-authorization/SKILL.md) |
| Injection | [injection-checking](./skills/injection-checking/SKILL.md) | [xss-cross-site-scripting](./skills/xss-cross-site-scripting/SKILL.md), [sqli-sql-injection](./skills/sqli-sql-injection/SKILL.md), [ssrf-server-side-request-forgery](./skills/ssrf-server-side-request-forgery/SKILL.md) |
| File Access | [file-access-vuln](./skills/file-access-vuln/SKILL.md) | [upload-insecure-files](./skills/upload-insecure-files/SKILL.md), [path-traversal-lfi](./skills/path-traversal-lfi/SKILL.md) |
| Business Logic | [business-logic-vuln](./skills/business-logic-vuln/SKILL.md) | [business-logic-vulnerabilities](./skills/business-logic-vulnerabilities/SKILL.md) |

## Repository Structure

```text
hack-skills/
├── README.md
├── README_CN.md
└── skills/
    ├── BUGBOUNTY_SKILLS.md
    ├── hack/
    │   └── SKILL.md
    ├── recon-for-sec/
    │   └── SKILL.md
    ├── api-sec/
    │   └── SKILL.md
    ├── auth-sec/
    │   └── SKILL.md
    ├── injection-checking/
    │   └── SKILL.md
    ├── file-access-vuln/
    │   └── SKILL.md
    ├── business-logic-vuln/
    │   └── SKILL.md
    ├── api-recon-and-docs/
    │   └── SKILL.md
    ├── authbypass-authentication-flaws/
    │   └── SKILL.md
    ├── jwt-oauth-token-attacks/
    │   └── SKILL.md
    ├── xss-cross-site-scripting/
    │   └── SKILL.md
    └── recon-and-methodology/
        └── SKILL.md
```

Directory notes:

- `hack/`: Master entry, install and use first.
- `recon-for-sec/`, `api-sec/`, `auth-sec/`, `injection-checking/`, `file-access-vuln/`, `business-logic-vuln/`: Six stable category entries.
- Other semantic directories such as `xss-cross-site-scripting/`, `api-auth-and-jwt-abuse/`, `recon-and-methodology/`, `upload-insecure-files/` are all directly loadable deep topic skills.
- The former payload-selection / brute-selection / API mid-routing helper skills have been merged into main topics or category entries to reduce entry noise and loader decision burden.

In other words, this repository is no longer "category subdirectories stuffed with scattered files", but a unified flat skill pool — with a deliberately preserved small entry layer.

Full index: `skills/BUGBOUNTY_SKILLS.md`.

## Skill Selection Guide

If you observe the following symptoms, start from these entry points:

| Symptom | Recommended Entry | Notes |
|---|---|---|
| New target, insufficient information | [recon-for-sec](./skills/recon-for-sec/SKILL.md) | Start with methodology and asset understanding |
| REST API, GraphQL, mobile backend | [api-sec](./skills/api-sec/SKILL.md) | Route to recon, authz, token, or GraphQL first |
| Login, password reset, 2FA, JWT, OAuth, object permission boundaries | [auth-sec](./skills/auth-sec/SKILL.md) | Distinguish authentication, authorization, and protocol configuration first |
| HTML/JS reflection, template expressions, dangerous parsing chains | [injection-checking](./skills/injection-checking/SKILL.md) | Determine if it's XSS, SQLi, SSRF, XXE, or SSTI first |
| File paths, download endpoints, upload flows | [file-access-vuln](./skills/file-access-vuln/SKILL.md) | Distinguish LFI/Traversal from Upload workflow first |
| Coupons, inventory, payments, state machines, multi-step flows | [business-logic-vuln](./skills/business-logic-vuln/SKILL.md) | Model by business rules and race conditions first |

## Installation

### General Installation

```bash
npx skills add yaklang/hack-skills
```

### Raw URL Installation

For tooling that supports pulling single-file skills. Pull the master entry first by default — not recommended to start directly from a deep topic:

```bash
curl -fsSL https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hack/SKILL.md
```

### Local Use as a Knowledge Base

```bash
git clone https://github.com/yaklang/hack-skills.git
cd hack-skills
```

Recommended reading order:

- [./skills/hack/SKILL.md](./skills/hack/SKILL.md)
- [skills/BUGBOUNTY_SKILLS.md](skills/BUGBOUNTY_SKILLS.md)
- [./skills/recon-for-sec/SKILL.md](./skills/recon-for-sec/SKILL.md)
- [./skills/recon-and-methodology/SKILL.md](./skills/recon-and-methodology/SKILL.md)

If you just want a more stable loader, prioritize having the loader hit `hack` and the six category entries; only target deep topic skills directly when the vulnerability symptom is already clear. The mid-tier helper skills have been significantly reduced and are no longer exposed to the loader by default.

## Design Principles

- Security knowledge takes priority over fancy packaging.
- Content auditability takes priority over quantity expansion.
- Prioritize authorized testing, legitimate research, and defensive verification scenarios.
- Directory names should convey security semantics at a glance, not be mechanical suffix stacking.

## Contributing

PRs are welcome. Key areas include:

- New vulnerability categories and high-value cases
- Better bug bounty methodologies
- Edge conditions that Agents easily overlook
- Risk annotations, terminology consistency, and content denoising

Contributions should ideally be:

- Verifiable
- Auditable
- Not encouraging unauthorized attacks
- Helpful for Agents to reason and execute more robustly in real tasks

