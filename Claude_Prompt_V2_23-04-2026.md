# Multi-Vendor Jewellery Marketplace — Claude Advisor Prompt

You are acting as my strategic and technical advisor for building a **multi-vendor online jewellery marketplace platform** on **Magento 2.4.6**. I am relatively new to running a business, so beyond answering my questions, I expect you to proactively share suggestions, flag risks, point out things I might be overlooking, and recommend best practices throughout our collaboration — treat me as a founder who needs both the big picture and the fine print.

---

## Context

**This is a greenfield project.** An earlier version of this platform existed but is being fully discarded — no previous code, scope, milestones, or architecture is being carried forward. We are starting from a clean slate with a fresh project, new scope, and new deliverables. However, since a prior version existed, I may occasionally reference how things worked before — treat those as background context, not constraints. Every decision should be evaluated on its own merit for this new build.

## Business Model in Brief

I am building a platform (think marketplace) where multiple jewellers, brands, and sellers can onboard, list their jewellery products, and sell directly to end consumers. My role is that of the **platform owner/operator** — I provide the technology, the storefront, the trust layer, and the operational backbone. Revenue will come from commissions, subscriptions, or a hybrid model (advise me on what works best for this vertical).

## Technology

The platform will be built on **Magento 2.4.6** (Adobe Commerce / Open Source — advise which edition suits better and why). All operations are **online-only** — no physical retail component at the initial stage.

---

## Platform Components

The platform consists of the following distinct components. Every phase of our work — journey mapping, technical decisions, scope, and milestones — must account for all of these and clearly specify which component each feature, flow, or task belongs to:

1. **Mobile App (Customer-facing)** — Native or hybrid app for end consumers to browse, purchase, track orders, and engage with the platform. The suggested technology is Flutter/Dart (you can advise on which approach suits better and why, but the preference is Flutter).

2. **Client Web (Customer-facing website)** — The Magento storefront for end consumers accessing via browser. Clarify upfront whether seller login/dashboard lives here or is separated out (see point 3), and recommend which approach is better and why. We have 2 options (Angular headless or Magento default web) out of which we could finalise the technology based on merits.

3. **Seller Portal** — Dedicated interface for vendors/sellers to onboard, manage catalogues, view orders, track payouts, and handle their storefront operations. This may be a separate standalone web application or a section within the Client Web — advise on the best approach for scalability, security, and user experience. Also explore if any activity required for this setup has been overlooked by me.

4. **Admin Terminal** — The platform operator's (my team's) back-office panel for managing vendors, approvals, commissions, disputes, platform-wide configurations, reporting, and overrides. This will likely extend or customise the Magento Admin panel — advise on how far native Magento admin can be stretched vs. when a custom admin frontend makes more sense. Also explore if any activity required for this setup has been overlooked by me.

5. **Magento APIs / Service Layer** — The backend engine powering all of the above. This includes Magento's REST/GraphQL APIs, custom API development, third-party integrations, and any middleware or orchestration layer needed to serve the Mobile App, Client Web, Seller Portal, and Admin Terminal consistently. Advise on a headless vs. traditional architecture and the trade-offs for our use case.

6. **System Integrity (Sub-Component)** — This may not be a separate component but is nonetheless crucial. Consider the technical aspects of security, data integrity, performance optimisation, backups, and other areas of the platform that may go undiscovered by me.

For every feature or flow we discuss, explicitly tag which component(s) it touches. Where a single flow spans multiple components (e.g., seller lists a product → admin approves → customer sees it on app and web), map the responsibility of each component clearly.

---

## Platform Roles, Governance & Operations

The following areas define what the business needs to function — independent of technology. These must be understood and resolved before translating into technical scope. They are organised business-first: commercial model → operations → compliance.

---

### Layer 1 — Business Knowledge & Operations

*"What does this business need to run, regardless of technology?"*

#### 1. Platform Revenue & Monetisation Strategy

Beyond commissions, define the full monetisation architecture. Cover: commission model (flat percentage, category-based slabs, tiered by seller volume, or hybrid), seller subscription tiers (free vs. paid plans with different listing limits, visibility, or commission rates), promoted/featured listing placements (seller pays to appear higher in search or on homepage — auction-based or fixed-price?), banner or spotlight advertising sold to sellers or external brands, premium tools or services (professional photography service, catalogue management assistance), and whether transaction fees (separate from commission) apply. Advise on which revenue streams are appropriate for launch vs. which to architect for but activate later. For each stream, specify where it surfaces (Admin Terminal for configuration, Seller Portal for purchase/management, Client Web and Mobile App for display).

#### 2. Pricing Engine & Live Rate Handling

Jewellery pricing is fundamentally different from standard e-commerce — prices are often tied to fluctuating metal rates (gold, silver, platinum) plus making charges, stone charges, and GST applied on different components differently. Define how the platform should handle pricing: does the platform provide a centralised live-rate feed that sellers' listings auto-calculate from, or do sellers set their own final prices manually? What is the cart-to-checkout price-lock policy — does the price freeze at cart-add, at checkout initiation, or at payment confirmation? How are rate fluctuations communicated to the customer? Also cover GST calculation logic (GST on gold value vs. making charges are taxed differently) and how the invoice should break this down. Advise on third-party rate feed providers for Indian bullion rates.

#### 3. Commission, Payout & Financial Operations

Define the platform's revenue mechanics and financial operations end-to-end. Cover: commission model (flat percentage, category-based slabs, tiered by seller volume, or hybrid), how commission is calculated on each order (on product value, on total including shipping, before or after returns?), payout cycle to sellers (daily, weekly, fortnightly — recommend what's standard), deductions before payout (commission, TDS, returns adjustment, penalties), payout reconciliation and reporting for sellers, and refund flow mechanics (who bears the cost — platform, seller, or split?). Also cover how the platform handles GST invoicing — platform commission attracts GST, marketplace TCS obligations under GST law, and whether the platform needs to issue invoices on behalf of sellers or sellers issue their own. Flag any compliance requirements specific to Indian marketplace e-commerce (ONDC implications, Consumer Protection E-Commerce Rules, FDI policy for marketplace model).

#### 4. Seller Onboarding & Verification Workflow

Define the complete seller onboarding journey end-to-end — from a new seller expressing interest to their first product going live. Cover: application/registration, required document collection (GST certificate, PAN, BIS registration, bank details for payout, business address proof), verification and approval workflow on the admin side, seller agreement/terms acceptance, orientation or training (self-serve guide, video walkthrough, or live session?), first catalogue upload and review by admin before going live, and whether there should be a probation period with limited visibility or features. Also advise on whether sellers should be tiered (e.g., new vs. verified vs. premium) and what benefits or restrictions each tier carries.

#### 5. Seller Performance Management & Accountability

Define how the platform monitors and manages seller quality over time. Cover: seller performance scorecard (metrics — order fulfilment rate, shipping SLA adherence, return rate, customer rating, response time to queries), automated warnings and penalty triggers (e.g., if fulfilment rate drops below X%, seller gets a warning), consequences ladder (warning → reduced visibility → temporary suspension → permanent deactivation), seller rehabilitation path (how a suspended seller can return to good standing), and incentive structures for high-performing sellers (featured placement, lower commission tier, badges). Specify where this surfaces — Admin Terminal for platform oversight, Seller Portal for seller self-monitoring.

#### 6. Catalogue Taxonomy & Attribute Standardisation

A marketplace with multiple sellers needs a unified product taxonomy to ensure consistent search, filtering, and comparison. Define a standardised catalogue schema for jewellery — covering categories (rings, necklaces, bangles, earrings, etc.), mandatory attributes (metal type, purity, gross weight, net weight, stone details, sizing), optional attributes (occasion, gender, collection name), and how sellers map their products into this schema during listing. Advise on whether the platform should enforce a fixed taxonomy with dropdowns/selections or allow free-text with AI-assisted normalisation. Also cover how product variants (same design in different sizes or metal purities) should be structured.

#### 7. Content & Media Governance

Jewellery is a visual-first category — inconsistent product imagery will erode buyer trust immediately. Define platform-wide media standards: mandatory image resolution, aspect ratios, background requirements (e.g., white/neutral), required angles (front, side, worn-on-model), video and 360° view specs if applicable. Specify the enforcement mechanism — automated validation at upload (file size, dimensions, format), manual review by a moderator role, or both. Define the rejection-and-resubmission flow for non-compliant media. Also advise on whether the platform should offer sellers a media toolkit or guidelines document as part of onboarding.

#### 8. Trust, Authenticity & Certification

Online jewellery purchase has a high trust barrier. Define how the platform establishes and communicates authenticity. Cover: BIS hallmark verification (is it mandatory for listing?), purity certificates, gemstone certification (GIA, IGI, etc.), and how these documents are uploaded by sellers, verified/approved by admin, and displayed to customers. Should the platform offer a trust badge or certification seal system? Advise on whether the platform should mandate a standard return/exchange guarantee or leave it to individual sellers, and the trade-offs of each approach. Also consider a product authenticity dispute flow — what happens if a customer claims a product is not as certified?

#### 9. Inventory Management & Stock Synchronisation

Define how inventory is managed across the platform. Cover: how sellers update stock (manual, bulk upload, real-time API sync from their own systems), what happens when stock reaches zero (auto-delist, show "out of stock", notify wishlisted customers when back?), how one-of-a-kind/unique piece inventory is handled differently from repeatable/manufactured designs, and the oversell prevention mechanism (what if two customers attempt checkout on the last unit simultaneously?). Also advise on whether the platform should support multi-channel inventory sync for sellers who list on other platforms (Amazon, their own site) — and the architectural implications if yes.

#### 10. Order Lifecycle & State Machine

Define the complete order state machine — every possible state an order can pass through from placement to final closure. Cover at minimum: placed, payment pending, payment confirmed, seller acknowledged, processing/packing, ready to ship, shipped, in transit, out for delivery, delivered, return requested, return approved/rejected, return in transit, return received, inspection passed/failed, refund initiated, refund completed, cancelled (by customer / by seller / by platform), and any dispute-hold or escalation-hold states. For each state, define: who triggers the transition (customer, seller, admin, system/automation), which components are involved, what notifications fire, and what the valid next states are. This state machine is the architectural backbone — all components must align to it.

#### 11. Shipping, Logistics & Transit Insurance

Jewellery has unique logistics requirements — high value, small form factor, theft risk. Define the shipping and delivery strategy: which logistics partners are suitable for insured high-value shipments (BlueDart, DTDC, FedEx, specialised partners like Sequel Logistics for valuables), mandatory transit insurance (who bears the cost — platform, seller, or buyer?), tamper-proof and branded packaging standards, OTP-verified or signature-verified delivery, and real-time tracking integration. Cover shipping cost structure — free shipping above threshold, flat rate, seller-defined, or weight/value-based. Also define the reverse logistics flow for returns — who arranges pickup, insurance on return transit, and inspection process on receipt.

#### 12. Payments, Financing & High-Value Transaction Handling

Jewellery purchases are high-value — payment strategy must reflect this. Define supported payment methods: UPI, credit/debit cards, net banking, platform wallet (if any), and advise on COD feasibility and risk for jewellery. Cover EMI options (card-based EMI, no-cost EMI partnerships with banks, third-party BNPL providers like Simpl, ZestMoney, LazyPay), and the integration approach for each. Define payment failure and retry flow, partial payment or pay-in-instalments model (e.g., advance + balance before shipping), and fraud detection on unusually large transactions. Also cover PCI-DSS compliance scope — what the platform must handle vs. what the payment gateway handles.

#### 13. Dispute Resolution & Escalation Framework

Define a structured dispute resolution framework — not just ticketing, but a clear escalation ladder with defined authority at each level. Cover: what types of disputes can arise (order not received, product not as described, authenticity challenge, wrong item, damaged in transit, seller not responding), who handles Level 1 (support agent), Level 2 (supervisor/manager), and Level 3 (platform operator decision), what SLAs apply at each level, what actions each level is authorised to take (refund, replacement, seller penalty, listing suspension), and how the outcome is communicated to both parties. Also define the evidence collection mechanism — photos, unboxing videos, certificates — and where this is captured (Mobile App, Client Web).

#### 14. Fraud Detection & Risk Management

Define the fraud and risk management framework for both buyer-side and seller-side. Cover: payment fraud detection (integration with payment gateway fraud tools, velocity checks on high-value orders, address mismatch flags), order fraud (fake orders, COD non-acceptance patterns), return fraud (customer returns a different or tampered product — inspection and evidence workflow), seller fraud (counterfeit listings, inflated pricing, fake inventory), and Anti-Money Laundering considerations for high-value gold transactions (thresholds, reporting obligations if applicable). Advise on what can be handled through rules and flags in the MVP vs. what needs dedicated fraud tooling later.

#### 15. Legal, Compliance & Policy Framework

Flag every area where the platform requires legal documentation, regulatory compliance, or policy definition. At minimum cover: platform Terms of Service and Privacy Policy, seller agreement/contract, Consumer Protection (E-Commerce) Rules 2020 compliance (display requirements, grievance officer appointment, return/refund obligations), Digital Personal Data Protection Act (DPDP) compliance for customer and seller data, FDI policy compliance for marketplace model (platform cannot own inventory or influence pricing), BIS Hallmarking Act obligations, GST and TCS compliance for marketplace operators, and any RBI guidelines relevant to payment handling or escrow. Claude should clearly flag where it can provide general guidance vs. where professional legal counsel is mandatory — and list those items as action items for me.

#### 16. Data Ownership, Privacy & Portability

Define clear data ownership and access boundaries. Cover: what customer data sellers can see (full address for shipping, but masked phone/email to prevent off-platform dealing?), what data the platform retains vs. what is seller-owned, what happens to a seller's data (product listings, order history, reviews) when they voluntarily leave or are deactivated, whether sellers can export their data (DPDP Act portability implications), and what customer data the platform can use for marketing, analytics, and personalisation. These decisions have architectural impact — data masking, access control layers, and export tooling must be designed in, not bolted on.

#### 17. Role Identification & Activity Mapping

Before diving into flows, identify every distinct user role the platform requires for smooth end-to-end operations — not just the obvious three (customer, seller, admin). Think about operational roles that sit behind the scenes. For example: who moderates catalogue quality and ensures product images meet a consistent standard (resolution, ratio, background)? Who handles customer support tickets and seller escalations — and does that need a dedicated support team role with its own interface? Who manages payouts, reconciliation, and financial disputes? Who handles vendor onboarding verification and KYC approvals? For each role you identify, define: what activities they perform, which component(s) they operate on, what permissions and access boundaries they need, and how their workflow hands off to or depends on other roles. Also flag where a single person might wear multiple hats in a lean team vs. where the role absolutely needs a dedicated person from day one.

#### 18. Seller-Platform Communication Channel

Define the communication infrastructure between the platform and its sellers, and between buyers and sellers. Cover: how does the platform operations team communicate with sellers beyond automated notifications — is there an internal messaging system, or is it email/phone-based? How does a seller raise a query or dispute with the platform (ticket system, chat, dedicated account manager)? Do buyers and sellers communicate directly (e.g., product enquiry before purchase, customisation discussion) — and if yes, is it through a platform-mediated messaging system (to prevent off-platform dealing) or external? For each channel, specify which component it lives on and how the conversation is logged for audit and dispute reference.

#### 19. Platform Launch & Go-Live Strategy

Advise on a phased launch strategy rather than a big-bang go-live. Define: what constitutes a viable soft launch (minimum number of sellers, minimum catalogue size, geographic scope), whether a closed beta with invite-only customers makes sense before public launch, what metrics determine readiness to move from beta to public, and what the rollback plan is if critical issues surface post-launch. This should inform how milestones are structured — the final milestone should produce a launch-ready platform, not just a feature-complete one.

---

### Layer 2 — Technical & Infrastructure

*"How does technology enable everything in Layer 1?"*

#### 20. Notifications & Communication Strategy

Map out the complete notification and communication framework across all roles and components. For every significant event in the platform lifecycle (order placed, shipped, delivered, returned, payout processed, KYC approved/rejected, ticket raised/replied/escalated, new seller onboarded, listing approved/rejected, etc.), define: who gets notified, through which channel (email, SMS, push notification, in-app alert), and whether the communication template is platform-controlled or customisable by the seller. Advise on the technology for this — transactional email service, SMS gateway, push notification service — and how it integrates with the Magento service layer.

#### 21. Reporting & Analytics per Role

Define what reporting and analytics each role needs access to, and on which component it surfaces. For example: the platform admin needs GMV, active sellers, commission revenue, dispute rates, and platform health metrics on the Admin Terminal. Sellers need their own sales performance, payout history, return rates, and listing performance on the Seller Portal. The support team needs ticket volume, resolution time, and SLA compliance. Advise on whether Magento's native reporting covers any of this, what needs custom dashboards, and whether a BI tool integration (e.g., Metabase, Google Looker Studio) is worth considering from the start or can be deferred.

#### 22. Audit Trail & Activity Logging

Given the financial nature of transactions and multi-role access, define what actions across the platform must be logged with a full audit trail (who, what, when, from which component). At minimum this should cover: admin overrides (manual refunds, commission adjustments, seller suspension), seller catalogue changes (price changes, listing edits, stock updates), order status changes, payout modifications, dispute resolutions, and role/permission changes. Advise on log retention policy, searchability for the admin team, and whether this data should live in Magento's database or a separate logging/observability stack.

#### 23. Platform Configuration & Feature Flags

Define what aspects of the platform must be configurable by the admin team without requiring a code deployment. Cover: commission rates and slabs, shipping rules and free-shipping thresholds, payout cycle settings, category and taxonomy management, homepage and banner content management, notification templates, seller onboarding document requirements, return window durations, and any business rule that is likely to change based on market feedback. Also advise on a feature flag system — the ability to enable/disable features for specific sellers, customer segments, or regions without redeployment. Specify how much of this Magento's native configuration covers vs. what needs custom admin tooling.

#### 24. Environment, DevOps & Release Strategy

Define the development and deployment infrastructure. Cover: environment strategy (local development → staging → UAT → production — or more?), CI/CD pipeline approach, code branching and release strategy (GitFlow, trunk-based), database migration handling across environments, who approves production deployments, hotfix protocol for critical bugs on live platform (especially during peak sale events like Diwali or Akshaya Tritiya), and rollback procedure. Also advise on containerisation (Docker/Kubernetes) and whether it's warranted for Magento at this scale, and hosting recommendation (AWS, GCP, or managed Magento hosting). This should align with the milestone delivery plan — each milestone should be deployable to at least staging.

#### 25. Disaster Recovery, Backup & Business Continuity

Define the platform's resilience and recovery strategy. Cover: database backup frequency and retention policy, media/asset backup (product images, certificates), disaster recovery environment (warm standby, cold standby, or cloud-based auto-failover), RTO (Recovery Time Objective) and RPO (Recovery Point Objective) targets appropriate for an e-commerce platform, incident response protocol (who is notified, escalation ladder, communication to customers and sellers during downtime), and whether the hosting architecture should be multi-AZ or multi-region from the start. This ties into the System Integrity sub-component — make the recommendations concrete.

---

### Open-Ended Discovery Instruction

Beyond the areas explicitly listed above, proactively identify and recommend any customer-facing features, engagement mechanics, or marketplace capabilities that are standard or differentiating for an online jewellery marketplace — do not limit yourself to only what I've mentioned. If you believe a feature matters for launch or should be architecturally planned for, surface it with your reasoning.

---

## What I Need From You, in Sequence

### Phase 1 — Platform Journey & Flow (Bird's Eye View)

Map out the complete platform journey from **every role's perspective** (as identified in the Roles, Governance & Operations section above) — **across all five components and the System Integrity sub-component**. Cover the entire lifecycle: onboarding, catalogue management, discovery, purchase, fulfilment, returns, payouts, dispute resolution, and any other flow you think is essential for a jewellery marketplace. For each flow, indicate which components are involved and what role each plays. Present this as a clear, high-level flow before we drill down.

### Phase 2 — Technical Footprint

Based on the journey above, outline the technology stack, integrations, and architectural decisions needed **per component and for the platform as a whole**. This includes but is not limited to: Magento multi-vendor module/extension strategy, Mobile App technology choice (React Native / Flutter / native — recommend one but stick to Flutter), Seller Portal technology (Magento-embedded vs. standalone Angular consuming APIs), API architecture (REST vs. GraphQL, headless considerations), payment gateway, logistics/shipping, KYC/trust verification for vendors, catalogue & media handling (high-res jewellery imagery, 360° views, video), SEO, performance, security (PCI-DSS, data protection), and any third-party services. Flag what Magento handles natively vs. what needs custom development or third-party extensions, and specify which component each decision impacts. Kindly explore and be open to suggesting any additional considerations, backing them with use cases that prove their merits.

### Phase 3 — Detailed Flow Drill-Down

Take the bird's eye view from Phase 1 and drill into every nook and corner — edge cases, decision points, conditional flows, failure scenarios, and admin overrides. **For each flow, break down the interaction between components** (e.g., what the Mobile App sends to the API, what the API validates, what the Admin Terminal displays for approval). Note where business rules need my input and where you can recommend a standard approach. Ask me clarifying questions wherever my decision is needed before proceeding.

### Phase 4 — Scope of Work (SoW) Structure

Convert the finalised flows and technical footprint into a structured Scope of Work document. **Organise the SoW by component** — each component (Mobile App, Client Web, Seller Portal, Admin Terminal, APIs/Services) should have its own section with modules listed under it. Each section should clearly state what is in-scope and what is explicitly out-of-scope or Open Item for this version of the platform. Cross-component dependencies should also be called out.

### Phase 5 — Milestone Breakdown (6–7 Milestones)

Break the entire SoW into **6 to 7 development milestones**, sequenced logically so that each milestone produces a demonstrable, testable deliverable. For each milestone, provide:

- Milestone objective (what it achieves)
- **Component-wise task breakdown** (what is being built/delivered in Mobile App, Client Web, Seller Portal, Admin Terminal, and APIs for that milestone)
- Functionalities / tasks included (drilled down from the SoW)
- Dependencies on previous milestones
- Estimated complexity indicator (light / medium / heavy)
- Deliverables at milestone completion

Structure milestones so that the **API/Service layer leads** (built or stubbed first) since all other components depend on it. Recommend whether any component can be deferred to a later milestone without blocking others (e.g., Mobile App after Client Web is stable).

---

## Standing Instructions for Our Collaboration

- Always share your opinion or recommendation before asking me to decide — I want to learn from your reasoning.
- If something is industry-standard or a known best practice in e-commerce / marketplace platforms, tell me so and suggest we follow it unless I have a reason not to.
- Flag any flow or decision that has legal, compliance, or financial implications (BIS hallmarking, GST on marketplace commissions, consumer protection rules, etc.).
- If at any point I am going down a path that adds unnecessary complexity for an MVP/first release, call it out and suggest what can be deferred to a later phase.
- When recommending build vs. buy (custom code vs. extension vs. third-party SaaS), always state the trade-off clearly.
- Keep outputs structured and document-ready — I will be using these directly to brief my development team.

---

> **Kick-off:** Let's begin with **Phase 1**. Map out the bird's eye view of the platform journey across all five components and one Sub-Component, and share your initial thoughts or suggestions on the business model and component architecture as well.
