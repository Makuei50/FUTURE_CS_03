# API Security Risk Analysis — Future Interns Cyber Security Task 3 (2026)

A read-only API security risk analysis performed against two public test APIs, conducted in the style of a professional API security audit for a SaaS client.

## Author
Makuei Geu Makuei

## Objective
Analyze public/test APIs for common API security risks, assess authentication and access control, explain risks in business terms, and propose remediation — without performing any exploitation, bypass, or denial-of-service testing.

## APIs Tested
- **JSONPlaceholder** — https://jsonplaceholder.typicode.com (open test API, no authentication)
- **ReqRes** — https://reqres.in (test API requiring an `x-api-key`)

## Tools Used
- **Postman** — request construction, header/authentication testing, response inspection
- **Browser** — reviewing published API documentation
- **Microsoft Word** — report documentation

## Scope
**In scope:**
- Read-only GET requests against publicly documented demo endpoints
- Authentication and access control inspection
- Header, token, and response inspection
- Documentation-based analysis

**Out of scope (not performed):**
- Exploitation or authentication bypass attempts
- Flooding / denial-of-service testing
- Testing of private or production systems

## Methodology
1. Selected two public test APIs with contrasting authentication models.
2. Reviewed each API's public documentation.
3. Sent baseline unauthenticated requests to observe default access behavior.
4. Obtained and applied a valid API key where required, then re-tested.
5. Inspected response bodies for volume/sensitivity of exposed data.
6. Tested invalid and edge-case inputs (non-existent IDs, non-numeric IDs).
7. Tested cross-resource requests to check for object-level authorization (IDOR).
8. Sent repeated rapid requests to check for rate limiting.
9. Classified each result by risk category, severity, business impact, and remediation.

## Summary of Findings

| # | API | Finding | Risk Category | Severity |
|---|-----|---------|---------------|----------|
| 1 | JSONPlaceholder | Unauthenticated access to full user PII dataset | Open/Unauthenticated Endpoint; Excessive Data Exposure | Medium (High in production) |
| 2 | JSONPlaceholder | Safe error handling on invalid/non-existent IDs | Input Validation | Pass |
| 3 | JSONPlaceholder | No ownership checks on posts/comments (IDOR pattern) | Broken Object Level Authorization | Medium (High in production) |
| 4 | ReqRes | Proper authentication enforcement + data minimization | Authentication | Pass |
| 5 | ReqRes | Safe error handling on invalid/non-existent IDs | Input Validation | Pass |
| 6 | ReqRes | No rate limiting observed on repeated requests | Missing Rate Limiting | Medium |

Full detail, business impact, and remediation guidance for each finding is documented in the report:
📄 [`API_Security_Risk_Analysis_Report.docx`](./API_Security_Risk_Analysis_Report.docx)

## Repository Structure

```
.
├── README.md
├── API_Security_Risk_Analysis_Report.docx
└── screenshots/
    ├── jsonplaceholder/
    │   ├── 01-users-endpoint.png
    │   ├── 02-invalid-id-404.png
    │   ├── 03-posts-by-userid.png
    │   └── 04-comments-by-postid.png
    └── reqres/
        ├── 01-unauthenticated-401.png
        ├── 02-authenticated-users.png
        ├── 03-invalid-id-404.png
        └── 04-rate-limit-test.png
```

## Ethics & Disclaimer
All testing in this project was performed exclusively against publicly available demo/test APIs explicitly intended for learning and testing purposes. No production systems, private APIs, or real user data were accessed. No exploitation, bypass, or denial-of-service techniques were used at any point.

## Reference Frameworks
Findings in this analysis are informed by, and mapped where applicable to, the [OWASP API Security Top 10](https://github.com/OWASP/API-Security) and the [API Security Checklist](https://github.com/shieldfy/API-Security-Checklist).
