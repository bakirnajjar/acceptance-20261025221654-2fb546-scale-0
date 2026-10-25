# Requirements analysis: customer password reset

**Stage:** `requirements_analysis` · **Schema version:** `1.0`

## Sources

- **S:** `user_story` / `user_story` / `characters 0-16000` — “As a customer I want to reset my password. Apply the curated recovery standard.”
- **K1:** `knowledge` / `467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3` / `v1, chunk 0` — account recovery standard v1, ACC-STD-01–03.
- **K2:** `knowledge` / `59efeb19-83f2-4ec6-bfd3-b4aeb7142930` / `v1, chunk 0` — account recovery standard v1, ACC-STD-01–03.

The source labels below resolve to the exact source references above. No attachments or approved prior-stage outputs were supplied.

## Requirements

### REQ-001 — Complete a customer password reset

**Statement:** A customer can complete a password reset so the new password replaces the previous password.

**Acceptance criterion:** Given an eligible customer and a valid, unused, unexpired reset link, when the customer completes a reset with an eligible new password, then the new password works for subsequent sign-in and the previous password no longer does.

**Sources:** S (story outcome).

### REQ-002 — Offer the request entry point

**Statement:** The sign-in page offers a “Forgot password?” link that starts a password reset request.

**Acceptance criterion:** Given the sign-in page, when a customer selects “Forgot password?”, then the password-reset request flow begins.

**Sources:** S; K1; K2 (ACC-STD-01).

### REQ-003 — Keep account existence undisclosed in the request response

**Statement:** A password-reset request returns an identical response whether the account exists or not.

**Acceptance criterion:** Given otherwise equivalent reset requests for an existing and a nonexistent account, when each request is submitted, then the externally observable request responses are identical.

**Sources:** S; K1; K2 (ACC-STD-01).

### REQ-004 — Limit reset requests

**Statement:** Password-reset requests are limited to five per account per hour.

**Acceptance criterion:** Given five accepted reset requests for the same account in a one-hour period, when a sixth is attempted in that period, then the sixth request is not accepted as another reset request for that account.

**Sources:** S; K1; K2 (ACC-STD-01).

### REQ-005 — Make reset links single-use

**Statement:** A reset link can complete at most one password reset.

**Acceptance criterion:** Given a valid, unexpired reset link that has completed a reset, when that link is used again, then it cannot complete another reset.

**Sources:** S; K1; K2 (ACC-STD-02).

### REQ-006 — Expire reset links after 30 minutes

**Statement:** A reset link expires 30 minutes after it is issued.

**Acceptance criterion:** Given a reset link issued at time T, when an attempt to complete a reset with it occurs at or after T plus 30 minutes, then the link cannot complete the reset.

**Sources:** S; K1; K2 (ACC-STD-02).

### REQ-007 — Sign out every active session on completion

**Statement:** Completing a password reset signs the account out of every active session.

**Acceptance criterion:** Given an account with one or more active sessions, when its password reset completes, then none of those sessions remains authenticated.

**Sources:** S; K1; K2 (ACC-STD-02).

### REQ-008 — Notify the account owner after success

**Statement:** The account owner is notified after every successful password reset.

**Acceptance criterion:** Given an account owner, when each password reset for that account succeeds, then the owner is notified for that successful reset.

**Sources:** S; K1; K2 (ACC-STD-03).

## Assumptions

1. acceptance-20261025221654-2fb546-skill-sentinel — the acceptance requirements skill produced this output.
2. The complete pinned story has no end marker. No attachments or approved prior-stage outputs were supplied, so there is no attachment marker or prior-stage reference to carry forward.
3. Only the customer password-reset outcome and the cited recovery-standard behaviors are in scope. No recovery-link delivery channel is prescribed; tests may arrange an issued link as a fixture.
4. No proof-of-ownership or verification protocol is specified; tests may arrange an eligible customer with a valid link as a precondition without waiving implementation security controls.
5. No new-password eligibility or complexity policy is specified; tests may use an eligible new password as a fixture without defining that policy.
6. For the five-per-account-per-hour limit, tests use five accepted requests and a sixth within an unambiguous shared one-hour period; neither window-boundary convention nor the response to a limited request is prescribed.
7. Notification to the owner is required after each successful reset, but no notification channel or message content is prescribed.

## Open questions (all non-blocking)

| Question | Assumption used instead |
| --- | --- |
| Through which channel is a reset link delivered? | No delivery channel is prescribed; test link behavior with an issued link as a fixture. |
| What proof-of-ownership or verification is required to issue or use a reset link? | No protocol is specified; test completion with an eligible customer and valid link without waiving implementation security controls. |
| What new-password eligibility or complexity rules apply? | No password policy is prescribed; use an eligible new password as a test fixture. |
| How is the hourly request window bounded, and what response is returned at the request limit? | Test five accepted requests and a sixth in an unambiguous shared one-hour period; do not prescribe boundary semantics or response. |
| Through which channel and with what content is the account owner notified? | Require notification after each successful reset without prescribing channel or content. |
