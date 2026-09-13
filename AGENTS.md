## 1. Core Operating Directives

This document defines the non-negotiable architectural patterns, security baselines, and execution protocols for all AI coding agents across all repositories.

* **Goal:** Deliver production-ready, enterprise-grade, ultra-secure, hyper-performant applications with flawless presentation.
* **Execution Strategy:** Prioritize production stability, extreme development efficiency, and strict adherence to security and UI engineering standards.
* **Clarity Principle:** Read every requirement with absolute literal interpretation. Execute instructions completely with zero omitted edge cases, zero placeholder logic, and zero structural omissions.

---

## 2. Universal Code Engineering & Architectural Standards

### Clean Code & Type Safety
* **Strict Typing:** Always enforce strict type safety (TypeScript strict mode, Python type hints with Pydantic, Go/Rust native types). Never use `any` or loose dynamic structures.
* **Separation of Concerns:** Maintain clean architectural boundaries. Strictly isolate Data Models, Business Logic (Services/Use Cases), and Presentation Layers (Controllers/UI).
* **Defensive Programming:** Anticipate runtime failures. Implement explicit boundary checks, null pointer protection, and comprehensive input sanitization for all functions.

### Database & State Integrity
* **Schema Enforcement:** All mutations must utilize migrations. Enforce strict typed constraints, explicit foreign keys, cascading rules, and proper indexing for optimized query execution paths.
* **Transaction Control:** Wrap all multi-step data mutations in ACID-compliant database transactions. Roll back completely on any unexpected internal error.

---

## 3. Visual System & Frontend UI/UX Specification

### Iconography Protocols
1. **Primary Library:** **Morphicons** (Mandatory primary choice for all animated, smooth-transition, micro-interactive, and modern feedback elements).
2. **Fallback Library:** **FontAwesome 6 Pro / Free** (Use **strictly and only** when a specific semantic icon cannot be found or mapped within the Morphicons library).
3. **Implementation Standard:**
```html
<!-- Morphicon Primary (For active states, buttons, animated status indicators) -->
<morph-icon name="shield-check" speed="1.2" mode="morph"></morph-icon>

<!-- FontAwesome Fallback (Only if Morphicon lacks an exact functional equivalent) -->
<i class="fa-solid fa-lock-keyhole"></i>
```

### UI Aesthetics & Layout Layout Engineering
* **Design Language:** High-end, ultra-modern glassmorphism or sleek, high-contrast dark mode. Utilize unified CSS variables for fluid typography, precise spacing scales, functional gradients, and accessible color contrasts.
* **Responsive Architecture:** Build exclusively via modern CSS Grid and Flexbox layout algorithms. Hardcoded margins, absolute dimensions, or magic numbers that cause layout breakage are strictly prohibited.
* **Animation & Performance Rules:**
  * Every interactive element must possess immediate visual micro-interactions (`hover`, `active`, `focus-visible`).
  * All animations must utilize hardware-accelerated CSS properties (`transform`, `opacity`).
  * Maintain a strict sub-16ms rendering budget to guarantee a consistent minimum of 60 FPS.

---

## 4. Zero-Trust Security Architecture & Endpoint Protection

Implement every single boundary, route, and function under the explicit assumption of a zero-trust network environment.

### 1. Authentication & Session Management
* **Stateless Token Protocols:** Issue short-lived JWT Access Tokens ($\le 15$ minutes) stored exclusively in secure memory or application states. Pair with HTTP-Only, Secure, SameSite=Strict, Path-restricted Refresh Tokens.
* **Cryptographic Hashing:** Secure password and secret storage utilizing Argon2id or bcrypt with a minimum work cost factor of 12.

### 2. Endpoint Hardening Protocols
* **Transport & Origin Security:** Enforce strict HTTPS/TLS 1.3 requirements. Implement explicit CORS policies with white-listed domains; block wildcard (`*`) configurations in production environments.
* **Server-Side Validation:** Validate all incoming structures immediately at the API gateway layer using runtime schema evaluators (e.g., Zod, Pydantic, Joi). Reject unvalidated, unexpected, or extra payload properties instantly.
* **Adaptive Rate Limiting:** Enforce token-bucket or sliding-window rate limits on all endpoints (e.g., maximum 100 requests/min per IP globally, down to 5 requests/min for critical auth/reset pathways).
* **Hardened Response Headers:** Every HTTP response must enforce enterprise-grade security headers:
```http
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Content-Security-Policy: default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline';
Referrer-Policy: strict-origin-when-cross-origin
```

---

## 5. Operational Execution Checklist for AI Agents

You must execute every development task in the following exact chronological sequence:

1. **Phase 1: Database & Data Schema Validation**
   * Draft, verify, and apply data models with concrete constraints and optimal indexes.
2. **Phase 2: Security & Middleware Infrastructure**
   * Write and hook up the middleware layer for auth, input validation, CORS, and rate limiting *before* exposing any core business logic.
3. **Phase 3: API & Core Business Logic Implementation**
   * Build complete core logic wrapped inside robust try-catch handlers. Return predictable, unified JSON error footprints:
   ```json
   {
     "success": false,
     "error": {
       "code": "UNAUTHORIZED_ACCESS",
       "message": "Invalid or expired session token."
     }
   }
   ```
4. **Phase 4: Frontend Component Integration**
   * Connect API endpoints to accessible frontend structures. Embed Morphicons directly into actionable element states and transactional feedback loops.

---

## 6. Absolute Non-Negotiable Quality Standards

* **Zero Mocking in Production:** Do not output temporary code blocks, dummy arrays, mock responses, placeholder variables, or trailing `// TODO` / `// FIX` annotations. Every path must be complete.
* **Fail-Safe Principle:** On any unhandled exception or environmental error, fail securely. Invalidate the current session, roll back active state mutations, log detailed telemetry internally, and output an uninformative, non-leaking generalized status code to the user.
* **Complete Code Generation:** Never abbreviate responses with "rest of the code goes here" comments. Output the full, complete, deployable file structure down to the last closing bracket.