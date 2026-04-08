# HACKING SKILLS / HackSkills — Master Index

> **AI LOAD INSTRUCTION**: This is the full-repository master index for HACKING SKILLS / HackSkills. Each `.skill.md` file is an AI-optimized attack playbook for one vulnerability class. Load the relevant skill file before testing for that vulnerability type. Do NOT rely on base training knowledge — load the specific skill first for expert-level techniques. For the primary SKILL.md installer entrypoint, see `skills/hack/SKILL.md`.

---

## SKILL FILES INDEX

| Category | File | Vulnerability Class | Key Topics |
|---|---|---|---|
| injection-sec | [injection-sec/XSS_Cross_Site_Scripting.skill.md](injection-sec/XSS_Cross_Site_Scripting.skill.md) | Cross-Site Scripting | Context matrix, multi-reflection, CSP bypass, blind XSS, WP→RCE, WAF bypass |
| injection-sec | [injection-sec/SQLi_SQL_Injection.skill.md](injection-sec/SQLi_SQL_Injection.skill.md) | SQL Injection | OOB exfil (Oracle UTL, MSSQL OpenRowSet), second-order, xp_cmdshell, blind |
| injection-sec | [injection-sec/SSRF_Server_Side_Request_Forgery.skill.md](injection-sec/SSRF_Server_Side_Request_Forgery.skill.md) | SSRF | Cloud metadata, IP encoding bypass, gopher/dict/file protocols, Redis via SSRF |
| injection-sec | [injection-sec/XXE_XML_External_Entity.skill.md](injection-sec/XXE_XML_External_Entity.skill.md) | XXE | OOB DTD exfil, SVG/Office XXE, XInclude, XXE→SSRF chain |
| injection-sec | [injection-sec/SSTI_Server_Side_Template_Injection.skill.md](injection-sec/SSTI_Server_Side_Template_Injection.skill.md) | SSTI | Polyglot probes, Jinja2 MRO chain, FreeMarker/Twig/ERB/Thymeleaf, Angular CSTI |
| authz-sec | [authz-sec/IDOR_Broken_Object_Authorization.skill.md](authz-sec/IDOR_Broken_Object_Authorization.skill.md) | IDOR/BOLA/BFLA | A-B testing, all ID locations, HTTP method escalation, mass assignment |
| injection-sec | [injection-sec/CMDi_Command_Injection.skill.md](injection-sec/CMDi_Command_Injection.skill.md) | OS Command Injection | All metacharacters, blind detection, OOB, reverse shells, filter bypass |
| file-access-sec | [file-access-sec/PathTraversal_LFI.skill.md](file-access-sec/PathTraversal_LFI.skill.md) | Path Traversal / LFI | Encoding chains, PHP wrappers (filter/input/data), log poisoning→RCE |
| auth-sec | [auth-sec/CSRF_Cross_Site_Request_Forgery.skill.md](auth-sec/CSRF_Cross_Site_Request_Forgery.skill.md) | CSRF | Token bypass patterns, SameSite bypass, JSON CSRF, OAuth state CSRF |
| api-sec | [api-sec/API_Security_Testing.skill.md](api-sec/API_Security_Testing.skill.md) | API Security | BOLA A-B test, BFLA, mass assignment, JWT attacks, GraphQL, rate limit bypass |
| auth-sec | [auth-sec/JWT_OAuth_Token_Attacks.skill.md](auth-sec/JWT_OAuth_Token_Attacks.skill.md) | JWT / OAuth | alg:none, RS256→HS256, secret crack, kid injection, OAuth redirect bypass |
| auth-sec | [auth-sec/AuthBypass_Authentication_Flaws.skill.md](auth-sec/AuthBypass_Authentication_Flaws.skill.md) | Authentication | SQLi login bypass, password reset flaws, 2FA bypass, session management |
| business-logic-sec | [business-logic-sec/BusinessLogic_Vulnerabilities.skill.md](business-logic-sec/BusinessLogic_Vulnerabilities.skill.md) | Business Logic | Race conditions, price manipulation, workflow bypass, coupon abuse |
| injection-sec | [injection-sec/NoSQL_Injection.skill.md](injection-sec/NoSQL_Injection.skill.md) | NoSQL Injection | MongoDB operator injection, $regex blind extraction, $where JS eval |
| recon-sec | [recon-sec/Recon_and_Methodology.skill.md](recon-sec/Recon_and_Methodology.skill.md) | Recon / Methodology | Subdomain enum, tech fingerprinting, endpoint discovery, zseano methodology |

---

## SKILL SELECTION GUIDE

### By Target Type

**Web App (traditional)**:
→ Load: XSS, SQLi, SSTI, CSRF, AuthBypass, PathTraversal, IDOR

**REST API / Mobile Backend**:
→ Load: API_Security_Testing, JWT_OAuth_Token_Attacks, IDOR, CSRF

**XML/SOAP Services**:
→ Load: XXE, SQLi (for SOAP), SSTI (FreeMarker/Velocity in Java backends)

**File Upload Features**:
→ Load: XSS (SVG/metadata), PathTraversal_LFI (file path control), CMDi (image processing)

**Payment / E-commerce**:
→ Load: BusinessLogic_Vulnerabilities, IDOR, API_Security_Testing

**Admin Panels**:
→ Load: AuthBypass, BFLA (in IDOR skill), SQLi, XSS

**Node.js / MongoDB Stack**:
→ Load: NoSQL_Injection, XSS, SSTI (Jade/Pug), CMDi

### By Observed Behavior

| Observation | Load Skill |
|---|---|
| Input reflected in HTML | XSS |
| Input in `<script>` tag | XSS (JS context) |
| Template expression: `{{7*7}}` | SSTI |
| Server makes outbound request | SSRF |
| XML accepted / parsed | XXE |
| File path in URL parameter | PathTraversal_LFI |
| Server executes system command | CMDi |
| API with object IDs | IDOR |
| Login endpoint | AuthBypass + SQLi |
| JWT token visible | JWT_OAuth |
| Multi-step payment/workflow | BusinessLogic |
| MongoDB backend | NoSQL_Injection |
| New program, unknown surface | Recon_and_Methodology first |

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
