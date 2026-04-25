# Feature Group 01 — Seller Onboarding

**Milestone:** M1 — Foundation
**Priority:** Must Have
**BA Owner:** —
**Last Updated:** 2026-04-25

---

## Purpose

This group covers the complete journey from a seller expressing interest in joining the MR platform to their first product going live. It includes identity verification, document collection, legal agreement, platform orientation, and the initial catalogue review gate.

---

## Features in This Group

| ID     | Feature                          | Status | Owner |
|--------|----------------------------------|--------|-------|
| MR-001 | KYC Document Upload              | draft  | —     |
| MR-002 | Seller Registration & Account Setup | — | —  |
| MR-003 | Seller Agreement & T&C Acceptance | —   | —     |
| MR-004 | Admin Verification & Approval Workflow | — | — |
| MR-005 | Seller Onboarding Orientation    | —      | —     |
| MR-006 | Probation Period & Tier Assignment | —    | —     |

> IDs MR-002 to MR-006 are placeholders — BRS files to be authored as the group is developed. Adjust IDs if features are added before these are started.

---

## Key Dependencies

- MR-001 (KYC Upload) must be accepted before MR-004 (Admin Verification) can begin.
- MR-003 (Seller Agreement) is a gate before any seller goes live on the platform.
- MR-006 (Probation / Tier) depends on MR-004 and informs Seller Portal Dashboard (Group 12).

---

## Out of Group Scope

- Seller performance scoring post-onboarding → Group 13 (Seller Performance Management)
- Payout account setup → Group 09 (Payout & Reconciliation)
- First product listing → Group 02 (Catalogue Management)
