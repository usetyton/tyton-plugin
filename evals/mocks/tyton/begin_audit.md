---
expect:
  url: string
---

{"schemaVersion":"1","kind":"session","status":"partial","url":"{{input.url}}","source":"agent_reported","reportSaved":false,"session":{"auditId":"audit-00000000000000000000000000000001","auditKey":"0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef","revision":0,"requestId":"6f1c2b9e-3d4a-4b5c-8d7e-9f0a1b2c3d4e"},"findings":[],"limitations":["This capability authorizes only this audit record, not access to the customer's website or permission to change it."],"nextActions":["Call audit_site with this session to inspect the public page."]}

Private audit session prepared; no report saved. Retain the capability and requestId before the first evidence write.
