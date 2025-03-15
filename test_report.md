# Test Report - Booking System Phase 1

## Introduction
- **Purpose:** Penetration testing of the Booking System (Phase 1).
- **Scope:** User registration, authentication, and input validation.
- **Tools Used:** OWASP ZAP, Docker.

## Summary
- **Key Findings:**
  1. SQL Injection vulnerability in the registration form.
  2. Weak session management.
  3. Lack of input validation leading to XSS.
- **Recommendations:**
  1. Use parameterized queries to prevent SQL injection.
  2. Strengthen session tokens and enforce HTTPS.
  3. Sanitize all user inputs.

## Findings and Categorization
- **Red (Critical):** SQL Injection.
- **Yellow (Medium):** Weak session management.
- **Green (Low):** Outdated library version.

## Appendices
- [ZAP Report](2025-03-15-ZAP-Report-.md)
