# BRS System Design — Multi-Vendor Jewellery Marketplace (MR)

**Date:** 2026-04-25
**Status:** Approved
**Author:** Kiran Prabhu

---

## 1. Purpose

This document defines the system and workflow for authoring, reviewing, approving, and maintaining Business Requirements Specification (BRS) documents for the MR (Marketplace) platform — a multi-vendor jewellery marketplace built on Magento 2.4.6.

The goal is to give the development team a **complete, unambiguous picture of every feature** before and during development, authored collaboratively by business analysts and product owners, and maintained as a living record through to post-implementation testing.

---

## 2. Core Principles

1. **Single source of truth** — The `/docs/wiki/` folder is the always-accurate, always-current picture of the platform. Nothing stale ever lives there.
2. **BRS before code** — Every feature has a written, stakeholder-accepted BRS before development begins, regardless of complexity.
3. **Already-built features are not exempt** — Features already implemented still get a BRS. For these, the BRS documents what exists and surfaces any gaps or deviations. Deviations are resolved collaboratively: either the BRS is updated to reflect the correct behaviour, or the source code is corrected. The wiki reflects the final agreed truth.
4. **Roles are always explicit** — Every BRS identifies every person or role that interacts with the feature — internal, external, operational — and defines their participation.
5. **Out of scope is mandatory** — Every BRS explicitly states what it does not cover. This prevents scope creep and protects sprint commitments.
6. **Testing closes the loop** — A BRS is not complete until QA has filled Section 10 (Testing Observations) and the wiki has been updated.

---

## 3. Repository Structure

```
/
├── docs/
│   ├── brs/                          ← BA workspace — active feature documents
│   │   ├── INDEX.md                  ← Master feature registry (status dashboard)
│   │   ├── _template.md              ← Canonical BRS template (copy to start)
│   │   │
│   │   ├── 01-seller-onboarding/
│   │   │   ├── GROUP.md              ← Feature group overview + child index
│   │   │   │
│   │   │   ├── MR-001-kyc-document-upload/    ← One folder per BRS
│   │   │   │   ├── MR-001-kyc-document-upload.md
│   │   │   │   └── assets/
│   │   │   │       ├── flow.svg      ← Feature flow diagram (SVG, embedded in BRS)
│   │   │   │       └── ux/           ← Wireframes, mockups, screen recordings
│   │   │   │
│   │   │   ├── MR-002-seller-agreement/
│   │   │   │   ├── MR-002-seller-agreement.md
│   │   │   │   └── assets/
│   │   │   │       ├── flow.svg
│   │   │   │       └── ux/
│   │   │   │
│   │   │   └── ...
│   │   │
│   │   ├── 02-catalogue-management/
│   │   │   ├── GROUP.md
│   │   │   └── ...
│   │   │
│   │   └── ...                       ← One numbered folder per feature group
│   │
│   └── wiki/                         ← Living system truth (post-implementation)
│       ├── INDEX.md                  ← Wiki master index
│       ├── 01-seller-onboarding/
│       │   └── MR-001-kyc-document-upload/
│       │       ├── MR-001-kyc-document-upload.md
│       │       └── assets/
│       │           ├── flow.svg
│       │           └── ux/
│       └── ...
│
├── .github/
│   ├── CODEOWNERS                    ← BA ownership per feature group folder
│   └── pull_request_template.md      ← PR checklist for BRS reviews
│
└── CONTRIBUTING.md                   ← BA workflow guide
```

**Key rules:**
- `/docs/brs/` is the working space. `/docs/wiki/` is the signed-off, post-tested record. Only verified features graduate to the wiki.
- Every BRS lives in its own folder named `MR-NNN-<slug>/`. This keeps the BRS document, flow diagram, and UX assets together as a single unit.
- The `assets/ux/` subfolder is created at BRS authoring time (even if empty) so there is always a clear place to drop wireframes, mockups, or screen recordings without restructuring later.

---

## 4. Feature ID Format

All features use a sequential identifier:

```
MR-NNN
```

Examples: `MR-001`, `MR-042`, `MR-123`

- IDs are assigned sequentially across the entire project — not per group
- The ID is permanent and never reused, even if a feature is deprecated
- The same ID is used in the BRS filename, Jira story, and wiki file

---

## 5. BRS File Template

Every child feature BRS (`/docs/brs/<group>/<id>-<slug>.md`) follows this structure:

```markdown
---
id: MR-NNN
title: <Feature Title>
feature_group: <Group Name>
milestone: M<N>
priority: must-have          # must-have | should-have | good-to-have
status: draft                # draft | in-review | accepted | implemented | verified
version: 0.1
jira_epic: JEWEL-XXX
jira_story: JEWEL-XXX
owner: <BA Name>
reviewers: [<Name>, <Name>]
components: []               # Mobile App | Client Web | Seller Portal | Admin Terminal | APIs
last_updated: YYYY-MM-DD
already_built: false         # true if feature exists in codebase before this BRS
---

## 1. Overview
One paragraph. What is this feature, why does it exist, what problem does it solve.

## 2. Roles & Personas
| Role | Type | Participation |
|------|------|---------------|
| <Role> | External User / Internal / System | <What they do in this feature> |

## 3. User Stories
- As a **<Role>**, I want to <action> so that <outcome>.

## 4. Functional Requirements
Numbered list of exact behaviours the system must exhibit.
1. ...
2. ...

## 5. Business Rules
Edge cases, constraints, and conditional logic specific to this feature.

## 6. Component Interaction Map
How each component participates in this feature:
- **Mobile App:** ...
- **Client Web:** ...
- **Seller Portal:** ...
- **Admin Terminal:** ...
- **APIs / Service Layer:** ...

## 7. Acceptance Criteria
- [ ] ...
- [ ] ...

## 8. Out of Scope
Explicit list of what this BRS does NOT cover.

## 9. Open Items / Decisions Pending
| # | Question | Owner | Due |
|---|----------|-------|-----|
| 1 | ... | ... | ... |

## 10. Testing Observations (Post-Implementation)
> Filled by QA after implementation. Triggers wiki update when complete.

| # | Observation | Severity | Resolution | Status |
|---|-------------|----------|------------|--------|

## 11. Change Log
| Version | Date | Author | Summary |
|---------|------|--------|---------|
| 0.1 | YYYY-MM-DD | <BA Name> | Initial draft |
```

---

## 6. Master INDEX.md Structure

Located at `/docs/brs/INDEX.md`, this is the control panel for the entire feature registry.

```markdown
# MR Feature Registry

Last updated: YYYY-MM-DD

| ID     | Feature                  | Group                  | Milestone | Priority     | Status      | Owner | Jira      |
|--------|--------------------------|------------------------|-----------|--------------|-------------|-------|-----------|
| MR-001 | KYC Document Upload      | Seller Onboarding      | M1        | must-have    | draft       | BA1   | JEWEL-101 |
| MR-002 | Seller Agreement         | Seller Onboarding      | M1        | must-have    | in-review   | BA1   | JEWEL-102 |
| MR-003 | Product Listing          | Catalogue Management   | M1        | must-have    | accepted    | BA2   | JEWEL-110 |
```

The INDEX is updated whenever a BRS status changes (on PR merge or status field update).

---

## 7. Feature Groups & Milestone Plan

### Milestone 1 — Foundation (Must Have)
| Group | Feature Group Name |
|-------|--------------------|
| 01 | Seller Onboarding |
| 02 | Catalogue Management |
| 03 | Pricing Engine |
| 04 | Order Lifecycle |
| 05 | Payments |
| 06 | Admin Terminal — Core |

### Milestone 2 — Operations (Must Have)
| Group | Feature Group Name |
|-------|--------------------|
| 07 | Shipping & Logistics |
| 08 | Returns & Refunds |
| 09 | Payout & Reconciliation |
| 10 | Trust & Authenticity |
| 11 | Dispute Resolution |

### Milestone 3 — Seller Experience (Should Have)
| Group | Feature Group Name |
|-------|--------------------|
| 12 | Seller Portal Dashboard |
| 13 | Seller Performance Management |
| 14 | Inventory Management |
| 15 | Seller-Platform Communications |

### Milestone 4 — Customer Experience (Should Have)
| Group | Feature Group Name |
|-------|--------------------|
| 16 | Customer Discovery |
| 17 | Wishlist & Alerts |
| 18 | Reviews & Ratings |
| 19 | Customer Support |

### Milestone 5 — Growth (Good to Have)
| Group | Feature Group Name |
|-------|--------------------|
| 20 | Monetisation & Promotions |
| 21 | Live Gold Rate Pricing |
| 22 | Notifications & Communications |
| 23 | Reporting & Analytics |
| 24 | Fraud Detection |
| 25 | Legal & Compliance Documentation |

### Milestone 6 — Platform Maturity (Good to Have)
| Group | Feature Group Name |
|-------|--------------------|
| 26 | Mobile App |
| 27 | Headless Storefront (Angular/PWA) |
| 28 | DevOps & Environments |
| 29 | Disaster Recovery & Business Continuity |
| 30 | Audit Trail & Logging |

> Feature groups and milestones are subject to evolution as features are defined. Deviations are resolved collaboratively between the BA team, product owner, and technical leads.

---

## 8. Git Collaboration Workflow

### Branch Naming
```
brs/MR-NNN-<short-slug>
```
Example: `brs/MR-001-kyc-document-upload`

### Workflow Steps
1. BA pulls latest `main`
2. Creates branch: `brs/MR-NNN-<slug>`
3. Copies `_template.md`, renames to `MR-NNN-<slug>.md`, places in correct group folder
4. Writes BRS, commits with message: `feat(brs): MR-NNN - <Feature Title> [draft]`
5. Updates `INDEX.md` with new entry
6. Raises PR — CODEOWNERS auto-assigns reviewers
7. Stakeholders review inline in PR comments
8. BA addresses comments, bumps version, updates changelog section
9. PR approved → merged to `main` → status updated to `accepted`
10. Dev team picks up the accepted BRS from `main`

### Post-Implementation
1. Dev marks BRS status as `implemented`
2. QA fills Section 10 (Testing Observations) via a new PR
3. BA + product owner review observations — resolve deviations in BRS or source code
4. Once verified, status flips to `verified`
5. BA copies final file to `/docs/wiki/<group>/` via PR
6. Wiki INDEX.md updated

### CODEOWNERS Example
```
docs/brs/01-seller-onboarding/   @ba-lead @seller-team-reviewer
docs/brs/02-catalogue-management/ @ba-lead @catalogue-reviewer
docs/wiki/                        @ba-lead @product-owner
```

---

## 9. PR Template (`.github/pull_request_template.md`)

```markdown
## BRS Review Checklist

- [ ] Feature ID (MR-NNN) assigned and added to INDEX.md
- [ ] All 11 sections of the template completed (no empty sections)
- [ ] Roles & Personas table covers all actors
- [ ] Open Items either resolved or have an owner + due date
- [ ] Jira epic and story linked in frontmatter
- [ ] Acceptance Criteria are testable (not vague)
- [ ] Out of Scope section explicitly written
- [ ] `already_built` flag set correctly
- [ ] Component Interaction Map filled for all relevant components
```

---

## 10. Deviation Handling (Already-Built Features)

When a BRS is written for a feature that is already implemented:

1. The `already_built: true` flag is set in the frontmatter
2. The BRS documents the **intended** behaviour (as it should be)
3. During acceptance review, the BA and tech lead compare BRS against actual implementation
4. Deviations are logged in a `## Deviations` sub-section under Section 10
5. Each deviation is resolved as one of:
   - **Accept** — BRS updated to reflect actual behaviour (implementation is correct)
   - **Fix** — Source code is corrected to match BRS (BRS intention is correct)
6. The wiki file reflects only the final, agreed, tested state

---

## 11. What Changes, What Stays

This system is intentionally designed to evolve. The following are fixed:
- ID format (`MR-NNN`)
- Template section numbering (Sections 1–11)
- The BRS → wiki promotion flow
- The `verified` status as the gate for wiki entry

The following can change collaboratively:
- Folder structure and group names
- Milestone assignments
- Feature groupings
- Template content within sections
- CODEOWNERS assignments

Any structural change should be reflected in an update to this design doc.
