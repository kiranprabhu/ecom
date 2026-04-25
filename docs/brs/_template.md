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

<!--
FOLDER STRUCTURE FOR THIS BRS
Each BRS lives in its own folder. When you copy this template, create the folder first:

  docs/brs/<NN-group-name>/MR-NNN-<slug>/
    MR-NNN-<slug>.md       ← this file
    assets/
      flow.svg             ← feature flow diagram (SVG, see Section 4)
      ux/                  ← wireframes, mockups, screen recordings (add as needed)

Example:
  docs/brs/01-seller-onboarding/MR-001-kyc-document-upload/
    MR-001-kyc-document-upload.md
    assets/
      flow.svg
      ux/
        login-screen-v1.png
        onboarding-wireframe.pdf
-->

## 1. Overview
One paragraph. What is this feature, why does it exist, what problem does it solve.

## 2. Roles & Personas
| Role | Type | Participation |
|------|------|---------------|
| <Role> | External User / Internal / System | <What they do in this feature> |

## 3. User Stories
- As a **<Role>**, I want to <action> so that <outcome>.

## 4. Feature Flow

End-to-end journey for this feature. The diagram is a hand-crafted SVG stored alongside this file — it renders in VS Code preview, Typora, GitHub, and any browser.

![Feature Flow](assets/flow.svg)

> To update the diagram: edit `assets/flow.svg` directly, or ask Claude to regenerate it.

**Key loops:**
- <loop 1 — what triggers it and where it re-enters the flow>
- <loop 2>

---

## 5. Functional Requirements
Numbered list of exact behaviours the system must exhibit.
1. ...
2. ...

## 6. Business Rules
Edge cases, constraints, and conditional logic specific to this feature.

## 7. Component Interaction Map
How each component participates in this feature:
- **Mobile App:** ...
- **Client Web:** ...
- **Seller Portal:** ...
- **Admin Terminal:** ...
- **APIs / Service Layer:** ...

## 8. Acceptance Criteria
- [ ] ...
- [ ] ...

## 9. Out of Scope
Explicit list of what this BRS does NOT cover.

## 10. Open Items / Decisions Pending
| # | Question | Owner | Due |
|---|----------|-------|-----|
| 1 | ... | ... | ... |

## 11. Testing Observations (Post-Implementation)
> Filled by QA after implementation. Triggers wiki update when complete.

| # | Observation | Severity | Resolution | Status |
|---|-------------|----------|------------|--------|

## 12. Change Log
| Version | Date | Author | Summary |
|---------|------|--------|---------|
| 0.1 | YYYY-MM-DD | <BA Name> | Initial draft |
