# Week 2 JWT Gap Analysis Report

## 1. Open Issues

### #725 — Security docs for OIDC and JWT IdPs
**Link:** https://github.com/kgateway-dev/kgateway.dev/issues/725  
**Status:** Open  
**Recommendation:** **KEEP** — Parent issue for the LFX project. Keep open until all IdP guides are done.

---

### #730 — Add JWT Validation Guide
**Link:** https://github.com/kgateway-dev/kgateway.dev/issues/730  
**Status:** Open  
**Recommendation:** **CLOSE** — Content already covered in `basic.md`.

---

### #739 — JWT Claims to Headers Guide
**Link:** https://github.com/kgateway-dev/kgateway.dev/issues/739  
**Status:** Open — Content ready  
**Recommendation:** **DECISION PENDING** — Awaiting Art's confirmation on canonical approach:
- If **TrafficPolicy** is canonical → SUBMIT #739, CLOSE #740
- If **GatewayExtension** is canonical → CLOSE #739, MERGE #740

---

### #735 — OIDC/OAuth2 Concepts Guide
**Link:** https://github.com/kgateway-dev/kgateway.dev/issues/735  
**Status:** Open  
**Recommendation:** **CLOSE** — PR #866 covers this content.

---

### #865 — Link Checker Report
**Link:** https://github.com/kgateway-dev/kgateway.dev/issues/865  
**Status:** Open  
**Recommendation:** **LOW PRIORITY** — Not JWT-specific. Address separately.

---

## 2. Open PRs

### #859 — Replace solo.io issuer with kgateway.dev
**Link:** https://github.com/kgateway-dev/kgateway.dev/pull/859  
**Status:** Open — Review Required  
**Recommendation:** **MERGE** — All fixes applied. Ready for final review.

---

### #740 — JWT claim extraction guide
**Link:** https://github.com/kgateway-dev/kgateway.dev/pull/740  
**Status:** Open — Review Required  
**Recommendation:** **DECISION PENDING** — Awaiting Art's confirmation on canonical approach:
- If **TrafficPolicy** is canonical → CLOSE #740 in favor of #739
- If **GatewayExtension** is canonical → MERGE #740, CLOSE #739

---

### #731 — JWT validation guide
**Link:** https://github.com/kgateway-dev/kgateway.dev/pull/731  
**Status:** Open — Review Required  
**Recommendation:** **CLOSE** — Duplicate of `basic.md`.

---

### #736 — OIDC/OAuth2 concepts guide
**Link:** https://github.com/kgateway-dev/kgateway.dev/pull/736  
**Status:** Open — Changes Requested  
**Recommendation:** **CLOSE** — Covered by PR #866.

---

### #772 — JWT release note example
**Link:** https://github.com/kgateway-dev/kgateway.dev/pull/772  
**Status:** Open — Changes Requested  
**Recommendation:** **LOW PRIORITY** — Not directly relevant to current work.

---

### #866 — Comprehensive OAuth2/OIDC integration guide
**Link:** https://github.com/kgateway-dev/kgateway.dev/pull/866  
**Status:** Open — Review Required  
**Recommendation:** **MERGE** with conditions:
- ✅ Aligns with OSS patterns (GatewayExtension + TrafficPolicy)
- ✅ Well-structured with sequence diagram
- ✅ Covers Keycloak as IdP example
- ⚠️ Add curl examples (follow `basic.md` pattern)
- ⚠️ Add troubleshooting section (follow `basic.md` pattern)
- ✅ Cross-link with #739 for claims extraction

---

## 3. Feature Gaps

API is fully documented in `basic.md`. No gaps identified.

| Feature | Documented |
|---------|------------|
| `jwt.providers` | ✅ |
| `jwt.providers[*].name` | ✅ |
| `jwt.providers[*].issuer` | ✅ |
| `jwt.providers[*].jwks.local` | ✅ |
| `jwt.providers[*].jwks.remote` | ✅ |
| `jwt.providers[*].audiences` | ✅ |
| `jwt.providers[*].claimsToHeaders` | ✅ |
| `jwt.providers[*].tokenSource` | ✅ |
| `jwt.providers[*].forwardToken` | ✅ |
| `jwt.validationMode` | ✅ |

---

## 4. Codebase Analysis

**Scope:** Searched `kgateway` codebase for JWT features and reviewed closed dev issues (ignoring `agentgateway`).

### Feature Verification

| Feature | Codebase | Docs | Status |
|---------|----------|------|--------|
| `JWTProvider`, `claimsToHeaders`, `remoteJwks`, `forwardToken`, `validationMode`, `tokenSource`, `audiences`, `JWKS` | ✅ All found | ✅ Documented | Complete |
| `OAuth2/OIDC` | ✅ Found (`oauth2.go`) | ✅ PR #866 covers | In review |
| `nested claims` (dot notation) | ❌ Not found | ❌ Not confirmed | Feature not verified |

### Key Closed Issues

| Issue | Impact |
|-------|--------|
| [#12930](https://github.com/kgateway-dev/kgateway/issues/12930) — Nested claims support | ❌ Not in codebase — no docs needed |
| [#12892](https://github.com/kgateway-dev/kgateway/issues/12892) — ValidationMode | ✅ Already documented |
| [#12996](https://github.com/kgateway-dev/kgateway/issues/12996) — forwardToken API change | ✅ Already documented |
| [#12891](https://github.com/kgateway-dev/kgateway/issues/12891) — Disable JWT | ⚠️ Could add to docs |
| [#13454](https://github.com/kgateway-dev/kgateway/issues/13454) — OAuth2 JWT parsing | ✅ PR #866 covers |
| [#14036](https://github.com/kgateway-dev/kgateway/issues/14036) — Two OAuth backends | ⚠️ Future docs update |
| [#9393](https://github.com/kgateway-dev/kgateway/issues/9393) — from_cookies | ⚠️ Not implemented |

### Verdict

| Aspect | Status |
|--------|--------|
| Codebase features match docs | ✅ Yes |
| Documentation gaps | ✅ None |
| OAuth2/OIDC coverage | ✅ PR #866 |
| Nested claims | ❌ Not in codebase — no docs |
| Items for maintainers | ⚠️ `disable` field, multiple OAuth backends |

**Conclusion:** All documented features are in the codebase. Nested claims are **not confirmed** — PR #740 documents them, but codebase search found no implementation. PR #866 aligns with codebase.

---

## 5. Summary

| Item | Action |
|------|--------|
| #725 | KEEP |
| #730 | CLOSE |
| #739 | PENDING (await Art) |
| #735 | CLOSE |
| #865 | LOW PRIORITY |
| #859 | MERGE |
| #740 | PENDING (await Art) |
| #731 | CLOSE |
| #736 | CLOSE |
| #772 | LOW PRIORITY |
| #866 | MERGE (with additions) |

---

*Report generated on June 24, 2026*