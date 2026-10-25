# Requirement inventory — assessment-to-contract mapping

Intermediate working inventory for task T001, run `95451d7e-33fe-4c4b-9e21-7e40e3541199`. This is not the `requirements_analysis` JSON contract or a product SDLC document.

## Evidence and contract coverage

- **S:** `{source_type: 'user_story', source_id: 'user_story', locator: 'characters 0-16000'}` — customer wants to reset a password under the curated recovery standard. The complete story has no end marker.
- **K1:** `{source_type: 'knowledge', source_id: '467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3', locator: 'v1, chunk 0'}` — account recovery standard, ACC-STD-01 through ACC-STD-03.
- **K2:** `{source_type: 'knowledge', source_id: '59efeb19-83f2-4ec6-bfd3-b4aeb7142930', locator: 'v1, chunk 0'}` — same standard and provisions as K1.

The source labels in every mapping below refer to these **exact source references**; both K1 and K2 must be carried into each supported requirement's `source_references` in the later contract. No attachment or approved prior-stage output was supplied. The assessment is in `assessment.md`; no approved-plan file was present in the artifact folder at inventory time. Its absence does not justify adding product scope.

## Atomic requirements for the later contract

### REQ-001 — Complete a customer password reset

**Statement:** A customer can complete a password reset so the new password replaces the previous password.

**Acceptance criterion:** Given an eligible customer and a valid, unused, unexpired reset link, when the customer completes a reset with an eligible new password, then the new password works for subsequent sign-in and the previous password no longer does.

**Source references:** S. The story establishes the core outcome; eligibility and valid link are test preconditions, not a prescribed proof-of-ownership or delivery mechanism.

### REQ-002 — Offer the request entry point

**Statement:** The sign-in page offers a “Forgot password?” link that starts a password reset request.

**Acceptance criterion:** Given the sign-in page, when a customer selects “Forgot password?”, then the password-reset request flow begins.

**Source references:** S; K1; K2 (ACC-STD-01).

### REQ-003 — Keep account existence undisclosed in the request response

**Statement:** A password-reset request returns an identical response whether the account exists or not.

**Acceptance criterion:** Given otherwise equivalent reset requests for an existing and a nonexistent account, when each request is submitted, then the externally observable request responses are identical.

**Source references:** S; K1; K2 (ACC-STD-01). No particular response text or status is prescribed.

### REQ-004 — Limit reset requests

**Statement:** Password-reset requests are limited to five per account per hour.

**Acceptance criterion:** Given five accepted reset requests for the same account in a one-hour period, when a sixth is attempted in that period, then the sixth request is not accepted as another reset request for that account.

**Source references:** S; K1; K2 (ACC-STD-01). The response to the limit and the exact window-boundary convention are not specified.

### REQ-005 — Make reset links single-use

**Statement:** A reset link can complete at most one password reset.

**Acceptance criterion:** Given a valid, unexpired reset link that has completed a reset, when that link is used again, then it cannot complete another reset.

**Source references:** S; K1; K2 (ACC-STD-02).

### REQ-006 — Expire reset links after 30 minutes

**Statement:** A reset link expires 30 minutes after it is issued.

**Acceptance criterion:** Given a reset link issued at time T, when an attempt to complete a reset with it occurs at or after T plus 30 minutes, then the link cannot complete the reset.

**Source references:** S; K1; K2 (ACC-STD-02).

### REQ-007 — Sign out every active session on completion

**Statement:** Completing a password reset signs the account out of every active session.

**Acceptance criterion:** Given an account with one or more active sessions, when its password reset completes, then none of those sessions remains authenticated.

**Source references:** S; K1; K2 (ACC-STD-02).

### REQ-008 — Notify the account owner after success

**Statement:** The account owner is notified after every successful password reset.

**Acceptance criterion:** Given an account owner, when each password reset for that account succeeds, then the owner is notified for that successful reset.

**Source references:** S; K1; K2 (ACC-STD-03). Notification channel and message are not prescribed.

## Scope assumptions for the later contract

- acceptance-20261025221654-2fb546-skill-sentinel — the acceptance requirements skill produced this output.
- No story end marker was present; no attachment or approved prior-stage output was supplied, so there is no attachment marker or prior-stage reference to carry forward.
- Only the customer reset outcome and the cited recovery-standard behaviors are in scope. Do not prescribe recovery delivery channel, proof-of-ownership protocol, password-complexity rules, rate-limit response, or notification channel.
- Tests may arrange an eligible customer, eligible new password, and issued valid link as preconditions without defining how those preconditions are established; this does not waive any implementation security controls.
- For the five-per-hour limit, test five accepted requests and a sixth within a clearly shared one-hour period; do not infer rolling versus fixed-window boundary behavior or the response to a limited request.

## Non-blocking open questions and assumptions used instead

| Question (non-blocking) | Assumption used for this inventory |
| --- | --- |
| Through which channel is a reset link delivered? | Do not prescribe delivery; test link-based behaviors with an issued link as a fixture. |
| What proof-of-ownership or verification is required to issue or use a link? | No protocol is specified; test successful completion only for an eligible customer with a valid link. |
| What new-password eligibility or complexity rules apply? | No rule is specified; use an eligible new password as a test fixture without defining a policy. |
| How is the hourly window bounded, and what response is returned at the request limit? | Test attempts within the same unambiguous one-hour period; leave boundary semantics and response unspecified. |
| Through which channel and with what content is the account owner notified? | Require notification after every success only; leave channel and content unspecified. |

The later JSON contract must use `schema_version: "1.0"`, `stage: "requirements_analysis"`, these stable `REQ-001`–`REQ-008` IDs, the exact evidence references above, nonempty Given/When/Then acceptance-criteria arrays, assumptions, and non-blocking open questions, following the pinned schema with no additional properties. **Do not write that contract as part of T001.**
