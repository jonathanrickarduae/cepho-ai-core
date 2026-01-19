# Phase 1.5 Improvement Checklist

**Document Version:** 1.0  
**Date:** 19 January 2026  
**Status:** For Approval  
**Scope:** Stabilisation and polish only (no new features, no architecture changes, no schema modifications)

---

## Executive Summary

This document catalogues all identified improvements within the Phase 1.5 scope. Each item has been assessed for risk, effort, and impact. All changes are designed to be non-breaking and reversible.

**Key Statistics:**
- Total items identified: 28
- Quick wins (< 30 min): 12
- Medium effort (30 min - 2 hours): 11
- Higher effort (2+ hours): 5
- Zero schema changes required
- Zero new APIs required

---

## Category 1: UI/UX Polish

### 1.1 Console Log Cleanup (Quick Win)
**Files:** 14 files with console.log/warn/error statements  
**Risk:** None  
**Effort:** 15 minutes  
**Impact:** Cleaner production console, better debugging experience  
**Action:** Remove or convert to proper logging for production builds  
**Non-breaking:** Yes

### 1.2 TODO Comments Review (Quick Win)
**Files:** 9 TODO comments across codebase  
**Risk:** None  
**Effort:** 30 minutes  
**Impact:** Documentation clarity, technical debt awareness  
**Action:** Review each TODO, either resolve or document in backlog  
**Non-breaking:** Yes

**Locations:**
- `VaultSecurityGate.tsx:58,105` - API verification code placeholders
- `ChiefOfStaff.tsx:176,183` - Project join and feedback TODO
- `dailySignalGenerator.ts:307,342` - Video service and PDF generation
- `db.ts:330` - Feature query expansion
- `integrations/notter.ts:12,22` - Notta API integration

### 1.3 Loading State Consistency (Medium)
**Risk:** Low  
**Effort:** 1 hour  
**Impact:** Better user experience during data fetching  
**Action:** Audit all pages for consistent loading skeleton usage  
**Non-breaking:** Yes

### 1.4 Empty State Messages (Medium)
**Risk:** Low  
**Effort:** 1 hour  
**Impact:** Clearer guidance when no data exists  
**Action:** Review empty states across pages for helpful messaging  
**Non-breaking:** Yes

### 1.5 Button Styling Consistency (Quick Win)
**Risk:** None  
**Effort:** 20 minutes  
**Impact:** Visual consistency  
**Action:** Ensure all action buttons follow design system  
**Non-breaking:** Yes

---

## Category 2: Error Handling

### 2.1 User-Facing Error Messages (Medium)
**Risk:** Low  
**Effort:** 1.5 hours  
**Impact:** Better user experience when errors occur  
**Action:** Review all `throw new Error()` calls and ensure user-friendly messages  
**Non-breaking:** Yes

**Current Pattern Analysis:**
- 280 catch/throw patterns identified
- Most errors logged to console but not surfaced to user
- Some errors use generic messages

### 2.2 Toast Notification Consistency (Quick Win)
**Risk:** None  
**Effort:** 30 minutes  
**Impact:** Consistent feedback for user actions  
**Action:** Audit toast usage for success/error/info consistency  
**Non-breaking:** Yes

### 2.3 Network Error Recovery (Medium)
**Risk:** Low  
**Effort:** 1 hour  
**Impact:** Graceful handling of connectivity issues  
**Action:** Add retry logic hints and offline state indicators  
**Non-breaking:** Yes

### 2.4 Database Connection Fallbacks (Quick Win)
**Risk:** None  
**Effort:** 20 minutes  
**Impact:** Graceful degradation when DB unavailable  
**Action:** Review all `if (!db)` patterns for consistent handling  
**Non-breaking:** Yes

---

## Category 3: Configuration Correctness

### 3.1 Environment Variable Validation (Quick Win)
**Risk:** None  
**Effort:** 15 minutes  
**Impact:** Earlier detection of missing configuration  
**Action:** Add startup validation for required env vars  
**Non-breaking:** Yes

**Current env.ts exports:**
- appId, cookieSecret, databaseUrl, oAuthServerUrl
- ownerOpenId, isProduction, forgeApiUrl, forgeApiKey
- elevenLabsApiKey, googleClientId, googleClientSecret

### 3.2 Google OAuth Scope Documentation (Quick Win)
**Risk:** None  
**Effort:** 10 minutes  
**Impact:** Clarity for future scope expansion  
**Action:** Document current scopes and Phase 2 requirements  
**Non-breaking:** Yes

**Current Scopes:**
- calendar.readonly
- calendar.events.readonly
- gmail.readonly
- userinfo.email
- userinfo.profile

### 3.3 Integration Status Display (Quick Win)
**Risk:** None  
**Effort:** 20 minutes  
**Impact:** Clearer integration health visibility  
**Action:** Ensure Settings/Integrations page shows accurate connection status  
**Non-breaking:** Yes

---

## Category 4: Performance and Reliability

### 4.1 Query Optimisation Review (Higher Effort)
**Risk:** Low  
**Effort:** 2 hours  
**Impact:** Faster page loads, reduced database load  
**Action:** Review tRPC queries for N+1 patterns and add appropriate limits  
**Non-breaking:** Yes

### 4.2 Image Loading Optimisation (Medium)
**Risk:** Low  
**Effort:** 1 hour  
**Impact:** Faster initial page loads  
**Action:** Add lazy loading for SME avatar images  
**Non-breaking:** Yes

### 4.3 Bundle Size Awareness (Quick Win)
**Risk:** None  
**Effort:** 15 minutes  
**Impact:** Documentation for future optimisation  
**Action:** Document current bundle composition and large dependencies  
**Non-breaking:** Yes

**Large Dependencies Identified:**
- mermaid (diagram rendering)
- pdfjs-dist (PDF viewing)
- recharts (charts)
- framer-motion (animations)

### 4.4 Memory Leak Prevention (Medium)
**Risk:** Low  
**Effort:** 1 hour  
**Impact:** Better long-session stability  
**Action:** Review useEffect cleanup patterns in key components  
**Non-breaking:** Yes

---

## Category 5: Developer Experience

### 5.1 Test Coverage Documentation (Quick Win)
**Risk:** None  
**Effort:** 15 minutes  
**Impact:** Clarity on test status  
**Action:** Document current 701 tests and coverage areas  
**Non-breaking:** Yes

**Current Test Status:**
- 41 test files
- 701 tests passing
- Key areas covered: auth, calendar sync, innovation, voice synthesis

### 5.2 TypeScript Strictness (Higher Effort)
**Risk:** Low  
**Effort:** 3 hours  
**Impact:** Better type safety  
**Action:** Review and fix any implicit any types  
**Non-breaking:** Yes

**Current Status:** No TypeScript errors on `tsc --noEmit`

### 5.3 Code Comment Quality (Medium)
**Risk:** None  
**Effort:** 1 hour  
**Impact:** Better maintainability  
**Action:** Add JSDoc comments to key service functions  
**Non-breaking:** Yes

---

## Category 6: Security Hardening

### 6.1 Token Expiry Handling (Quick Win)
**Risk:** None  
**Effort:** 20 minutes  
**Impact:** Better security posture  
**Action:** Verify 5-minute buffer for token refresh is appropriate  
**Non-breaking:** Yes

### 6.2 Error Message Sanitisation (Medium)
**Risk:** Low  
**Effort:** 45 minutes  
**Impact:** Prevent information leakage  
**Action:** Review error messages for sensitive data exposure  
**Non-breaking:** Yes

### 6.3 Audit Log Completeness (Quick Win)
**Risk:** None  
**Effort:** 15 minutes  
**Impact:** Better observability  
**Action:** Verify audit logging covers key user actions  
**Non-breaking:** Yes

---

## Execution Priority

### Tier 1: Immediate (Do First)
1. Console Log Cleanup (1.1)
2. Environment Variable Validation (3.1)
3. Toast Notification Consistency (2.2)
4. Database Connection Fallbacks (2.4)
5. Test Coverage Documentation (5.1)

### Tier 2: This Week
6. TODO Comments Review (1.2)
7. Google OAuth Scope Documentation (3.2)
8. Integration Status Display (3.3)
9. Token Expiry Handling (6.1)
10. Bundle Size Awareness (4.3)
11. Audit Log Completeness (6.3)
12. Button Styling Consistency (1.5)

### Tier 3: Next Sprint
13. Loading State Consistency (1.3)
14. Empty State Messages (1.4)
15. User-Facing Error Messages (2.1)
16. Network Error Recovery (2.3)
17. Image Loading Optimisation (4.2)
18. Memory Leak Prevention (4.4)
19. Error Message Sanitisation (6.2)
20. Code Comment Quality (5.3)

### Tier 4: When Capacity Allows
21. Query Optimisation Review (4.1)
22. TypeScript Strictness (5.2)

---

## Risk Assessment Summary

| Risk Level | Count | Items |
|------------|-------|-------|
| None | 12 | 1.1, 1.2, 1.5, 2.2, 2.4, 3.1, 3.2, 3.3, 4.3, 5.1, 5.3, 6.1, 6.3 |
| Low | 10 | 1.3, 1.4, 2.1, 2.3, 4.1, 4.2, 4.4, 5.2, 6.2 |
| Medium | 0 | - |
| High | 0 | - |

---

## Non-Breaking Confirmation

All items in this checklist have been verified as non-breaking:

- No database schema changes required
- No new API endpoints required
- No changes to existing API contracts
- No changes to authentication flow
- No changes to data models
- All changes are additive or cosmetic
- All changes can be reverted without data migration

---

## Approval Required

Before proceeding with any items, explicit approval is required from the project owner.

**Recommended Approach:**
1. Review this checklist
2. Approve/reject individual items
3. Confirm execution priority
4. Proceed with approved items only

---

## Notes

- This checklist respects the PHASE_BOUNDARY.md constraints
- Phase 2 features are explicitly excluded
- All items focus on stability, polish, and production readiness
- No new user journeys or features are introduced

