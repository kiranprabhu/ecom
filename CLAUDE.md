# CLAUDE.md — MR Jewellery Marketplace

This file provides guidance to Claude Code when working in this repository.

---

## Project Overview

**MR** is a greenfield multi-vendor online jewellery marketplace platform built on **Magento 2.4.6**. Multiple jewellers, brands, and sellers can onboard, list jewellery products, and sell directly to end consumers. The platform owner provides the technology, storefront, trust layer, and operational backbone.

The full project brief is in: `Claude_Prompt_V2_23-04-2026.md`

---

## Platform Components

Every feature and BRS must specify which component(s) it touches:

1. **Mobile App** — Flutter/Dart, customer-facing
2. **Client Web** — Magento storefront (Angular headless or Magento default — TBD)
3. **Seller Portal** — Vendor interface for onboarding, catalogue, orders, payouts
4. **Admin Terminal** — Platform operator back-office (extends Magento Admin)
5. **APIs / Service Layer** — Magento REST/GraphQL + custom APIs powering all components
6. **System Integrity** — Security, performance, backups, data integrity (cross-cutting)

---

## Repository Structure

```
/
├── docs/
│   ├── brs/                  ← BA workspace — active BRS documents
│   │   ├── INDEX.md          ← Master feature registry
│   │   ├── _template.md      ← BRS template
│   │   └── NN-<group>/       ← One folder per feature group
│   │       ├── GROUP.md
│   │       └── MR-NNN-<slug>.md
│   │
│   └── wiki/                 ← Living system truth (post-implementation only)
│       └── NN-<group>/
│           └── MR-NNN-<slug>.md
│
├── .github/
│   ├── CODEOWNERS
│   └── pull_request_template.md
│
├── CONTRIBUTING.md
├── CLAUDE.md                 ← This file
└── Claude_Prompt_V2_23-04-2026.md  ← Full project brief
```

---

## BRS System

### Feature ID Format
```
MR-NNN   (e.g. MR-001, MR-042)
```
Sequential across the entire project. Same ID used in filename, Jira, and wiki.

### BRS Lifecycle
```
draft → in-review → accepted → implemented → verified → wiki
```
- Only `verified` features are promoted to `/docs/wiki/`
- The wiki is always the single source of truth — nothing stale lives there

### Key Rules
- Every feature gets a BRS — including already-built ones (`already_built: true` flag)
- Deviations between BRS and existing code are resolved collaboratively: fix the BRS or fix the code
- Section 8 (Out of Scope) is mandatory in every BRS
- Section 10 (Testing Observations) is filled by QA and gates wiki promotion

### Git Workflow
- Branch per BRS: `brs/MR-NNN-<slug>`
- PR = stakeholder review gate
- Merge to `main` = accepted

---

## Milestone Plan (Summary)

| Milestone | Theme | Priority |
|-----------|-------|----------|
| M1 | Foundation — Seller Onboarding, Catalogue, Pricing, Orders, Payments, Admin Core | Must Have |
| M2 | Operations — Shipping, Returns, Payouts, Trust, Disputes | Must Have |
| M3 | Seller Experience — Dashboard, Performance, Inventory, Comms | Should Have |
| M4 | Customer Experience — Discovery, Wishlist, Reviews, Support | Should Have |
| M5 | Growth — Promotions, Live Rates, Notifications, Analytics, Fraud, Legal | Good to Have |
| M6 | Platform Maturity — Mobile App, Headless Web, DevOps, DR, Audit | Good to Have |

Full milestone detail: `docs/superpowers/specs/2026-04-25-brs-system-design.md`

---

## Working Conventions

- Always use absolute paths in bash commands (shell cwd may differ from this project)
- New BRS files go in `/docs/brs/<group>/MR-NNN-<slug>.md`
- Never write to `/docs/wiki/` directly — wiki promotion happens only after QA sign-off
- The design system doc is the authority: `docs/superpowers/specs/2026-04-25-brs-system-design.md`
- Feature groups and milestones can evolve — update the design doc when they do
