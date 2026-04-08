# HACKING SKILLS / HackSkills — Loader Index

> **AI LOAD INSTRUCTION**: This file is the loader-oriented master index for HACKING SKILLS / HackSkills. Prefer the primary entry skill [hack/SKILL.md](./hack/SKILL.md), then a category router, and only then a deep topic skill. Do NOT start from the longest flat list of micro-skills unless the current evidence is already specific.

> Loader note: entry-layer skills now keep directory-consistent frontmatter names such as `hack`, `recon-for-sec`, `api-sec`, and `auth-sec`. Loader stability is handled by a reduced entry set plus converged `Entry P0 / Entry P1` descriptions, not by renaming skills away from their directory names.

---

## Primary Entry Skills

| Priority | Skill | Use For | Notes |
|---|---|---|---|
| P0 | [hack](./hack/SKILL.md) | 全局路由、阶段判断、跨类别切换 | 推荐默认起点 |
| P1 | [recon-for-sec](./recon-for-sec/SKILL.md) | 新目标、资产发现、方法论 | 当目标上下文不足时优先 |
| P1 | [api-sec](./api-sec/SKILL.md) | REST、GraphQL、移动端后端 | API 类问题的分类入口 |
| P1 | [auth-sec](./auth-sec/SKILL.md) | 登录、JWT、OAuth、IDOR、对象授权 | 认证授权类入口 |
| P1 | [injection-checking](./injection-checking/SKILL.md) | XSS、SQLi、SSRF、XXE、SSTI、CMDi、NoSQL | 注入类入口 |
| P1 | [file-access-vuln](./file-access-vuln/SKILL.md) | 上传、下载、路径控制、文件处理链 | 文件访问类入口 |
| P1 | [business-logic-vuln](./business-logic-vuln/SKILL.md) | 流程、价格、状态机、竞态 | 业务逻辑入口 |

## Category To Topic Map

这些是分类入口下最值得优先下钻的深度专题。原先的 payload-selection、brute-selection 一类短 skill 已并入主 skill，不再保留为独立入口。

| Category | Start Here | Deep Topics |
|---|---|---|
| Recon | [recon-for-sec](./recon-for-sec/SKILL.md) | [recon-and-methodology](./recon-and-methodology/SKILL.md) |
| API | [api-sec](./api-sec/SKILL.md) | [api-recon-and-docs](./api-recon-and-docs/SKILL.md), [api-authorization-and-bola](./api-authorization-and-bola/SKILL.md), [api-auth-and-jwt-abuse](./api-auth-and-jwt-abuse/SKILL.md), [graphql-and-hidden-parameters](./graphql-and-hidden-parameters/SKILL.md) |
| Auth | [auth-sec](./auth-sec/SKILL.md) | [authbypass-authentication-flaws](./authbypass-authentication-flaws/SKILL.md), [idor-broken-object-authorization](./idor-broken-object-authorization/SKILL.md), [jwt-oauth-token-attacks](./jwt-oauth-token-attacks/SKILL.md), [oauth-oidc-misconfiguration](./oauth-oidc-misconfiguration/SKILL.md), [cors-cross-origin-misconfiguration](./cors-cross-origin-misconfiguration/SKILL.md), [saml-sso-assertion-attacks](./saml-sso-assertion-attacks/SKILL.md) |
| Injection | [injection-checking](./injection-checking/SKILL.md) | [xss-cross-site-scripting](./xss-cross-site-scripting/SKILL.md), [sqli-sql-injection](./sqli-sql-injection/SKILL.md), [ssrf-server-side-request-forgery](./ssrf-server-side-request-forgery/SKILL.md), [xxe-xml-external-entity](./xxe-xml-external-entity/SKILL.md), [ssti-server-side-template-injection](./ssti-server-side-template-injection/SKILL.md), [cmdi-command-injection](./cmdi-command-injection/SKILL.md), [nosql-injection](./nosql-injection/SKILL.md) |
| File Access | [file-access-vuln](./file-access-vuln/SKILL.md) | [upload-insecure-files](./upload-insecure-files/SKILL.md), [path-traversal-lfi](./path-traversal-lfi/SKILL.md) |
| Business Logic | [business-logic-vuln](./business-logic-vuln/SKILL.md) | [business-logic-vulnerabilities](./business-logic-vulnerabilities/SKILL.md) |

## Deep Topic Index

当现象已经非常明确时，再直接加载这些深度专题 skill：

| Category | File | Vulnerability Class | Key Topics |
|---|---|---|---|
| injection-checking | [./xss-cross-site-scripting/SKILL.md](./xss-cross-site-scripting/SKILL.md) | Cross-Site Scripting | Context matrix, multi-reflection, CSP bypass, blind XSS, WP→RCE, WAF bypass |
| injection-checking | [./sqli-sql-injection/SKILL.md](./sqli-sql-injection/SKILL.md) | SQL Injection | OOB exfil (Oracle UTL, MSSQL OpenRowSet), second-order, xp_cmdshell, blind |
| injection-checking | [./ssrf-server-side-request-forgery/SKILL.md](./ssrf-server-side-request-forgery/SKILL.md) | SSRF | Cloud metadata, IP encoding bypass, gopher/dict/file protocols, Redis via SSRF |
| injection-checking | [./xxe-xml-external-entity/SKILL.md](./xxe-xml-external-entity/SKILL.md) | XXE | OOB DTD exfil, SVG/Office XXE, XInclude, XXE→SSRF chain |
| injection-checking | [./ssti-server-side-template-injection/SKILL.md](./ssti-server-side-template-injection/SKILL.md) | SSTI | Polyglot probes, Jinja2 MRO chain, FreeMarker/Twig/ERB/Thymeleaf, Angular CSTI |
| auth-sec | [./idor-broken-object-authorization/SKILL.md](./idor-broken-object-authorization/SKILL.md) | IDOR/BOLA/BFLA | A-B testing, all ID locations, HTTP method escalation, mass assignment |
| injection-checking | [./cmdi-command-injection/SKILL.md](./cmdi-command-injection/SKILL.md) | OS Command Injection | All metacharacters, blind detection, OOB, reverse shells, filter bypass |
| file-access-vuln | [./path-traversal-lfi/SKILL.md](./path-traversal-lfi/SKILL.md) | Path Traversal / LFI | Encoding chains, PHP wrappers (filter/input/data), log poisoning→RCE |
| auth-sec | [./csrf-cross-site-request-forgery/SKILL.md](./csrf-cross-site-request-forgery/SKILL.md) | CSRF | Token bypass patterns, SameSite bypass, JSON CSRF, OAuth state CSRF |
| auth-sec | [./jwt-oauth-token-attacks/SKILL.md](./jwt-oauth-token-attacks/SKILL.md) | JWT / OAuth | alg:none, RS256→HS256, secret crack, kid injection, OAuth redirect bypass |
| auth-sec | [./authbypass-authentication-flaws/SKILL.md](./authbypass-authentication-flaws/SKILL.md) | Authentication | SQLi login bypass, password reset flaws, 2FA bypass, session management |
| auth-sec | [./oauth-oidc-misconfiguration/SKILL.md](./oauth-oidc-misconfiguration/SKILL.md) | OAuth / OIDC Misconfiguration | redirect URI, state, nonce, PKCE, account binding, token audience |
| auth-sec | [./cors-cross-origin-misconfiguration/SKILL.md](./cors-cross-origin-misconfiguration/SKILL.md) | CORS Misconfiguration | reflected origin, credentialed CORS, allowlist bypass, readable APIs |
| auth-sec | [./saml-sso-assertion-attacks/SKILL.md](./saml-sso-assertion-attacks/SKILL.md) | SAML SSO | signature validation, assertion wrapping, audience, ACS, binding confusion |
| business-logic-vuln | [./business-logic-vulnerabilities/SKILL.md](./business-logic-vulnerabilities/SKILL.md) | Business Logic | Race conditions, price manipulation, workflow bypass, coupon abuse |
| file-access-vuln | [./upload-insecure-files/SKILL.md](./upload-insecure-files/SKILL.md) | Upload Insecure Files | Validation bypass, storage abuse, processing chains, overwrite, preview and sharing bugs |
| injection-checking | [./nosql-injection/SKILL.md](./nosql-injection/SKILL.md) | NoSQL Injection | MongoDB operator injection, $regex blind extraction, $where JS eval |
| recon-for-sec | [./recon-and-methodology/SKILL.md](./recon-and-methodology/SKILL.md) | Recon / Methodology | Subdomain enum, tech fingerprinting, endpoint discovery, zseano methodology |
| api-sec | [./api-recon-and-docs/SKILL.md](./api-recon-and-docs/SKILL.md) | API Recon | OpenAPI, Swagger, version drift, hidden docs, endpoint surface |
| api-sec | [./api-authorization-and-bola/SKILL.md](./api-authorization-and-bola/SKILL.md) | API Authorization | BOLA, BFLA, method abuse, nested resources, mass assignment |
| api-sec | [./api-auth-and-jwt-abuse/SKILL.md](./api-auth-and-jwt-abuse/SKILL.md) | API Auth / JWT | Token trust, header abuse, rate-limit bypass, claim misuse |
| api-sec | [./graphql-and-hidden-parameters/SKILL.md](./graphql-and-hidden-parameters/SKILL.md) | GraphQL / Hidden Parameters | Introspection, batching, undocumented fields, schema abuse |

---

## Entry Reduction Note

为减少 loader 入口噪音，以下类型的独立 skill 已并入主 skill：

- payload selection
- brute selection
- default credentials / username generation / port targeting
- API 中间路由型轻量 skill

现在优先保留三层：`hack` 总入口、分类入口、深度专题。

---

## SKILL SELECTION GUIDE

### By Target Type

| Target Type | Start With | Then Consider |
|---|---|---|
| Web App (traditional) | [injection-checking](./injection-checking/SKILL.md) | XSS, SQLi, SSTI, CSRF, Path Traversal, IDOR |
| REST API / Mobile Backend | [api-sec](./api-sec/SKILL.md) | API Security Testing, JWT/OAuth, IDOR, CSRF |
| XML/SOAP Services | [injection-checking](./injection-checking/SKILL.md) | XXE, SQLi, SSTI |
| File Upload Features | [file-access-vuln](./file-access-vuln/SKILL.md) | Upload Insecure Files, XSS, Path Traversal, CMDi |
| Payment / E-commerce | [business-logic-vuln](./business-logic-vuln/SKILL.md) | Business Logic, IDOR, API Security |
| Admin Panels | [auth-sec](./auth-sec/SKILL.md) | Authentication Bypass, BFLA/IDOR, SQLi, XSS |
| Node.js / MongoDB Stack | [injection-checking](./injection-checking/SKILL.md) | NoSQL Injection, XSS, SSTI, CMDi |

### By Observed Behavior

| Observation | Start With | Then Consider |
|---|---|---|
| Input reflected in HTML | [injection-checking](./injection-checking/SKILL.md) | XSS |
| Input in `<script>` tag | [injection-checking](./injection-checking/SKILL.md) | XSS (JS context) |
| Template expression: `{{7*7}}` | [injection-checking](./injection-checking/SKILL.md) | SSTI |
| Server makes outbound request | [injection-checking](./injection-checking/SKILL.md) | SSRF |
| XML accepted / parsed | [injection-checking](./injection-checking/SKILL.md) | XXE |
| File path in URL parameter | [file-access-vuln](./file-access-vuln/SKILL.md) | Path Traversal / LFI |
| Server executes system command | [injection-checking](./injection-checking/SKILL.md) | CMDi |
| API with object IDs | [api-sec](./api-sec/SKILL.md) | BOLA / IDOR |
| Login endpoint | [auth-sec](./auth-sec/SKILL.md) | Authentication Bypass, SQLi |
| JWT token visible | [auth-sec](./auth-sec/SKILL.md) | JWT / OAuth |
| Multi-step payment/workflow | [business-logic-vuln](./business-logic-vuln/SKILL.md) | Business Logic |
| MongoDB backend | [injection-checking](./injection-checking/SKILL.md) | NoSQL Injection |
| New program, unknown surface | [recon-for-sec](./recon-for-sec/SKILL.md) | Recon and Methodology |

---

## ESCALATION CHAINS (COMMON COMBOS)

```
XSS → CSRF (use XSS to extract CSRF token → perform CSRF)
XSS → Account Takeover (steal session cookie via fetch())
XSS → RCE (WordPress admin XSS → plugin editor → webshell)

SSRF → Cloud Metadata → Credential Theft → Full Cloud Compromise
SSRF → Internal Redis → Shell via crontab write

XXE → SSRF → Cloud Metadata
XXE → File Read → Credential Exposure → Database Access

IDOR → Mass Assignment → Privilege Escalation → Admin Access

SQLi → Auth Bypass → Admin Panel → XSS → RCE
SQLi (Oracle) → UTL_HTTP OOB → Data Exfiltration

JWT weak secret → Crack → Forge Admin JWT → Full Account Access
OAuth CSRF → Account Takeover

PathTraversal + LFI → Log Poisoning → PHP Code Execution → Reverse Shell
```

---

## EXPERT INTUITIONS (THINGS BASE MODELS MISS)

1. **The same filter exists everywhere**: if you find filtered XSS in search, try the same payload in file upload filenames, profile bio, error messages.

2. **WAF checks parameter values, not names**: inject in the parameter NAME, not value.

3. **OOB is the most reliable SQLi technique**: when in-band fails, UTL_INADDR for Oracle DNS exfil works through firewalls that block HTTP.

4. **BOLA = auth but no authz**: app authenticates the request but doesn't check if the authenticated user OWNS the object.

5. **JWT RS256 → HS256 confusion requires the public key**: get it from `/well-known/jwks.json` before attempting.

6. **Second-order vulnerabilities** are everywhere: data stored safely, retrieved "trusted", re-used in dangerous context.

7. **Race conditions** exploit the check-then-act window: always test "once-only" features (coupons, trial, password reset) with parallel requests.

8. **The 2-minute SameSite Lax exemption**: cookies issued in the last 2 minutes can be sent in cross-site POST — useful for CSRF timing attacks.

9. **API versioning**: when v2 patches a bug, test v1 — often still deployed and vulnerable.

10. **Business logic flaws have the best dollar-per-hour ratio**: they can't be scanned, persist longer, often yield P1/P2 payouts.
