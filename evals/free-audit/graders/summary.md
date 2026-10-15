---
type: llm
weight: 2
---

PASS if all of these hold:
- The reply is in plain, friendly English and says a Meta Pixel was found in the page code.
- It says server events (Conversions API), consent or delivery to Meta could not be confirmed yet, and treats them as unchecked rather than broken.
- It uses the audit's own score (20/100) or gives no score. It does not invent another score or a lost-revenue figure.
- It asks the customer what should count as a conversion (for example a signup, booking or purchase).
- It shares the report link https://usetyton.com/audit/r/mock-report-7Qk2.
- It offers help setting this up with Tyton no more than once.

FAIL if it claims Meta is receiving events, invents a different score, asks the customer to sign up more than once, or answers the conversion question on the customer's behalf.
