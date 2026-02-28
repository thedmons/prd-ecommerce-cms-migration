# PRD: E-Commerce CMS Platform Migration
**Author:** Thomas Edmons, Associate Product Manager
**Status:** Completed
**Timeline:** ~18 months | Late 2019 – Mid 2021
**Last Updated:** February 2026

---

## Table of Contents
1. [Overview](#overview)
2. [Problem Statement](#problem-statement)
3. [Goals & OKRs](#goals--okrs)
4. [User Personas](#user-personas)
5. [Scope](#scope)
6. [Solution Overview](#solution-overview)
7. [Technical Architecture](#technical-architecture)
8. [Key Requirements](#key-requirements)
9. [Out of Scope](#out-of-scope)
10. [Success Metrics](#success-metrics)
11. [Risks & Mitigations](#risks--mitigations)
12. [Dependencies](#dependencies)
13. [Open Questions & Decisions](#open-questions--decisions)
14. [Appendix](#appendix)

---

## Overview

This document defines the product requirements for the migration of a large home improvement retailer's e-commerce web platform — encompassing 250+ landing pages supporting online sales, savings, installation services, help, and brand content. The existing platform, built on Adobe Experience Manager (AEM) — a legacy monolithic CMS — was replaced with a modern composable architecture built on an in-house headless CMS, a React front-end UI, and Google Cloud Storage (GCS) for hosting and content delivery.

The project spanned approximately 18 months and addressed compounding reliability, performance, SEO, and content authoring challenges inherent to the monolithic AEM platform. A Black Friday outage on the legacy system elevated this migration to a business-critical priority.

---

## Problem Statement

The existing platform was built on Adobe Experience Manager (AEM), a legacy monolithic CMS that had grown increasingly difficult to maintain, scale, and author content within. Its tightly coupled architecture created compounding constraints across reliability, performance, developer flexibility, and content operations that could not be resolved without a full platform migration.

**Core pain points:**

**Site reliability:** The legacy AEM platform's dependence on aging infrastructure created instability under peak traffic conditions. A significant outage during Black Friday — one of the highest-traffic retail events of the year — directly impacted online sales and accelerated the migration timeline.

**Web performance:** The platform exhibited poor Core Web Vitals across mobile web, including slow Largest Contentful Paint (LCP) and high Cumulative Layout Shift (CLS). Data showed a significant and accelerating shift in customer traffic toward mobile, making mobile web performance a critical business priority — degraded scores on mobile directly impacted the browsing and purchasing experience for the retailer's fastest-growing traffic segment.

**SEO and discoverability:** 250+ landing pages were organized under a single subdirectory with inconsistent URL structures, making it difficult for search engines to crawl and index content effectively. Pages lacked proper schema metadata, reducing eligibility for rich search results and suppressing organic visibility.

**Content authoring:** The AEM platform required desktop and mobile web experiences to be authored separately, doubling the effort required for every content update. AEM's complexity created a steep learning curve and high operational overhead for content authors and merchandisers.

**Infrastructure and cloud migration:** The legacy platform was dependent on on-premises storage infrastructure, creating scalability constraints and operational overhead that cloud-native alternatives could eliminate. Migrating to the cloud was a strategic priority for the organization — both as a technology modernization initiative and as a meaningful driver of infrastructure cost savings. Moving to Google Cloud Storage directly supported this organizational objective while providing the reliability and scalability the platform required.

**Page ownership:** Historical ownership of page content was undocumented and poorly governed across the organization. Many stakeholder teams — including Legal, Privacy, and Installation Services — had no established working relationship with the digital team, creating significant coordination overhead during migration.

---

## Goals & OKRs

### Objective 1: Improve Platform Reliability
**KR:** Eliminate single-point-of-failure infrastructure dependencies that caused the Black Friday outage.
**KR:** Achieve ≥99.9% uptime SLA on the new platform through peak traffic events.

### Objective 2: Improve Web Performance and Core Web Vitals
**KR:** Achieve measurable improvement in LCP on mobile web across all migrated landing pages.
**KR:** Reduce CLS to within Google's "Good" threshold (≤0.1) across all migrated pages.
**KR:** Improve overall mobile Core Web Vitals scores to "Good" or "Needs Improvement" across the top 50 pages by traffic volume.

### Objective 3: Improve SEO and Organic Discoverability
**KR:** Restructure 250+ landing pages from a single flat subdirectory into 5 logical subdirectories aligned to site sections (Shop, Savings, Installation, Help, About).
**KR:** Implement schema metadata across all migrated pages to improve search engine eligibility for rich results.
**KR:** Preserve SEO equity across all migrated URLs via proper redirect mapping.

### Objective 5: Migrate from On-Premises to Cloud Infrastructure
**KR:** Fully decommission on-premises storage dependencies by migrating all static assets and content delivery to Google Cloud Storage.
**KR:** Achieve measurable infrastructure cost reduction relative to on-premises operational overhead.


**KR:** Eliminate the requirement to author desktop and mobile experiences separately — enable single-authoring with responsive output.
**KR:** Consolidate personalization segments into the CMS authoring workflow, replacing the Adobe Target dependency.

---

## User Personas

### Persona 1: Content Author / Merchandiser
**Who they are:** Content authors and merchandising teams responsible for a broad scope of digital content across the retailer's web presence — including 250+ landing pages spanning shop, savings, installation, help, and brand sections; static site pages such as the homepage, category pages, and consumer blog posts; targeted marketing banners; and a wide range of digital assets.
**Goals:** Publish and update content quickly without duplicating effort across desktop and mobile; manage personalization segments within a single workflow; maintain content accuracy and brand consistency across a high-volume, multi-format content operation.
**Pain points:** The legacy AEM platform required separate authoring for desktop and mobile experiences, doubling publishing effort for every update across an already extensive content portfolio. AEM's complexity created high operational overhead, and the volume and variety of content types — pages, banners, digital assets — made inefficient workflows especially costly at scale.
**Success looks like:** One authoring action publishes a responsive experience across all viewports. Personalization segments are configurable directly in the CMS without switching tools. The breadth of the team's content responsibilities is manageable within a single, streamlined authoring environment.

### Persona 2: Front-End / Platform Engineer
**Who they are:** Engineers responsible for building and maintaining the web platform and its integration with the in-house CMS.
**Goals:** Work in a modern, well-documented stack; reduce maintenance burden from legacy infrastructure; ship reliably without fear of outages under load.
**Pain points:** AEM's monolithic architecture tightly coupled content and presentation, limiting front-end flexibility and slowing development cycles. The legacy platform's infrastructure created reliability issues under peak traffic, culminating in a Black Friday outage.
**Success looks like:** A headless CMS architecture decouples content from the front end. GCS-backed infrastructure is reliable and scalable under peak retail traffic events.

### Persona 3: E-Commerce / Business Stakeholder
**Who they are:** Cross-functional teams including Marketing, Legal, Privacy, Installation Services, and other lines of business who own or contribute to landing page content.
**Goals:** Ensure their content is accurately represented, compliant, and live on the site; receive timely support from the digital team for content changes.
**Pain points:** Page content ownership was historically undocumented. Many teams had no established relationship with the digital organization and limited familiarity with web publishing processes.
**Success looks like:** Page ownership is documented and governed. Stakeholder teams have a clear process for submitting and reviewing content. Migration is completed without loss or misrepresentation of business-critical content.

### Persona 4: Site Visitor (End Customer)
**Who they are:** Online shoppers and customers visiting the retailer's website to browse products, find savings, learn about installation services, or get help.
**Goals:** Find relevant pages quickly via search or site navigation; experience fast, stable page loads on mobile; complete purchases or service bookings without friction.
**Pain points:** Slow LCP and high CLS on mobile web degraded the browsing experience. Poor URL structure and missing schema metadata made it harder for customers to find relevant pages through organic search.
**Success looks like:** Pages load fast and render stably on mobile. Organic search surfaces the right pages for the right queries. Navigation across site sections is intuitive and logically structured.

---

## Scope

### In Scope
- Migration of 250+ landing pages across 5 site sections: Shop, Savings, Installation, Help, and About
- URL restructuring from a single flat subdirectory to 5 logical subdirectories
- Implementation of schema metadata across all migrated pages
- SEO redirect mapping to preserve equity across all migrated URLs
- Front-end rebuild enabling responsive, single-authoring experiences
- Integration with the new in-house headless CMS
- Consolidation of personalization segments into the CMS authoring workflow (replacing Adobe Target)
- Page content ownership documentation and governance across all stakeholder teams
- Core Web Vitals benchmarking and validation pre- and post-migration
- Stakeholder coordination and UAT across Legal, Privacy, Installation Services, and other contributing teams

### Out of Scope
- Product detail pages (PDPs) and product listing pages (PLPs)
- Transactional / checkout flows
- Native mobile applications
- Back-end e-commerce systems (inventory, pricing, order management)
- Redesign of existing content — migration preserves existing content with structural and performance improvements

---

## Solution Overview

The new platform replaces Adobe Experience Manager's legacy monolithic architecture with a composable, microservices-oriented stack — an in-house headless CMS, a responsive React front-end UI, and Google Cloud Storage for hosting and static asset delivery — designed for reliability, performance, and authoring efficiency.

**Content layer (In-house headless CMS):** A purpose-built headless CMS replaces AEM's monolithic content and presentation layer. Decoupling content from the front end via API enables each layer to be independently deployed, scaled, and maintained. Content is authored once and delivered responsively across viewport sizes, eliminating the desktop/mobile dual-authoring workflow of the legacy platform. Personalization segments are integrated directly into the authoring interface, consolidating the Adobe Target dependency.

**UI layer (React / responsive front end):** The front end is rebuilt as a responsive React application, consuming content via CMS APIs. Responsive design eliminates the need for separate mobile and desktop content trees.

**Infrastructure layer (Google Cloud Storage):** GCS replaces on-premises storage infrastructure, fulfilling the organization's strategic priority to migrate to the cloud for both technology modernization and infrastructure cost reduction. GCS provides scalable, reliable static asset and content delivery hardened to support peak retail traffic events such as Black Friday without the reliability risks of the legacy on-prem environment.

**SEO and URL architecture:** 250+ pages are reorganized from a flat single-subdirectory structure into 5 logical subdirectories. Schema metadata is implemented across all pages. A comprehensive redirect map preserves SEO equity from legacy URLs.

**Page ownership governance:** A cross-functional content ownership initiative — driven in parallel with the migration — documented and assigned ownership of all 250+ pages across contributing business teams, enabling scalable content governance post-launch.

---

## Technical Architecture

```
                    ┌─────────────────────────────────────────┐
                    │         Content Authors / Merch          │
                    │      (In-House Headless CMS)             │
                    │  [ Replaces: AEM Monolithic CMS ]        │
                    │  [ Desktop + Mobile → Single Author ]    │
                    │  [ Personalization Segments Built-In ]   │
                    └──────────────────┬──────────────────────┘
                                       │ Content API (Microservice)
                    ┌──────────────────▼──────────────────────┐
                    │          React Front End                 │
                    │      (Responsive / Single Build)         │
                    │  [ Independently Deployed Microservice ] │
                    └──────────────────┬──────────────────────┘
                                       │
               ┌───────────────────────▼─────────────────────────┐
               │              Google Cloud Storage                │
               │       (Static Assets / Content Delivery)         │
               └───────────────────────┬─────────────────────────┘
                                       │
          ┌────────────────────────────▼──────────────────────────┐
          │                    URL Architecture                    │
          │   /shop  /savings  /install  /help  /about              │
          │         (5 Logical Subdirectories + Schema)            │
          └───────────────────────────────────────────────────────┘
```

---

## Key Requirements

### Functional Requirements

**Content Management**
- Authors must be able to publish a single content entry that renders responsively across desktop and mobile viewports
- Personalization segments must be configurable within the CMS authoring interface without requiring a separate tool
- Content preview must be available for both desktop and mobile viewports prior to publishing
- All 250+ pages must have a documented content owner assigned prior to migration cutover

**SEO and URL Architecture**
- All 250+ pages must be restructured into one of 5 logical subdirectories: /shop, /savings, /installation, /help, /about
- Schema metadata (e.g. breadcrumb, article, FAQ, product) must be implemented on all migrated pages appropriate to content type
- 301 redirects must be in place for all legacy URLs prior to cutover to preserve SEO equity
- Canonical tags must be correctly implemented across all migrated pages

**Front End**
- All migrated pages must render correctly and performantly across modern browsers and mobile viewports
- Core Web Vitals targets must be validated on mobile web prior to each page group cutover
- React components must consume content exclusively via CMS API — no hardcoded content in the front-end codebase

**Infrastructure**
- GCS must be configured for reliable static delivery under peak retail traffic conditions
- Infrastructure must support Black Friday and seasonal traffic spikes without degradation
- Uptime monitoring and alerting must be in place prior to launch

### Non-Functional Requirements
- LCP: measurable improvement over legacy baseline on mobile web across all migrated pages
- CLS: ≤0.1 across all migrated pages
- Uptime SLA: ≥99.9% on production environment
- SEO: zero loss of indexed pages post-migration (validated via Google Search Console)
- Migration completion: all 250+ pages migrated, validated, and ownership-documented by mid-2021

---

## Out of Scope

- Product detail pages, product listing pages, and transactional flows
- Back-end e-commerce systems (inventory, pricing, order management)
- Native mobile applications
- Content redesign — migration preserves existing content with structural and performance improvements only

---

## Success Metrics

| Metric | Baseline | Target | Status |
|---|---|---|---|
| Platform reliability (uptime) | Outage on Black Friday | ≥99.9% through peak events | ✅ Achieved |
| Mobile LCP | Poor (legacy baseline) | Measurable improvement | ✅ Achieved |
| Mobile CLS | Above threshold | ≤0.1 | ✅ Achieved |
| URL structure | 1 flat subdirectory | 5 logical subdirectories | ✅ Achieved |
| Schema metadata | Not implemented | Implemented across all pages | ✅ Achieved |
| SEO equity (redirects) | N/A | 100% of legacy URLs redirected | ✅ Achieved |
| Dual-authoring requirement | Desktop + mobile authored separately | Single authoring, responsive output | ✅ Achieved |
| Page ownership documentation | Undocumented | 100% of 250+ pages assigned | ✅ Achieved |
| On-premises storage dependency | Active | Fully migrated to GCS | ✅ Achieved |
| Infrastructure cost | On-prem overhead | Reduced via cloud migration | ✅ Achieved |

---

## Risks & Mitigations

**Risk: SEO equity loss during URL migration**
*Impact: High | Likelihood: Medium*
Restructuring 250+ pages across new subdirectories carries significant risk of losing organic search rankings if redirects are incomplete or improperly implemented.
*Mitigation:* Comprehensive redirect mapping was completed prior to cutover, with 301 redirects validated for every legacy URL. Google Search Console was monitored post-launch to identify and address any indexing gaps.

**Risk: Stakeholder coordination at scale**
*Impact: High | Likelihood: High (realized)*
250+ pages spanned content owned by teams across the organization — many of whom had no prior relationship with the digital team and limited familiarity with web publishing. Legal, Privacy, and Installation Services required significant onboarding and coordination.
*Mitigation:* A parallel content ownership initiative documented and assigned ownership across all pages before migration began. Structured review processes were established for each stakeholder group, enabling UAT and sign-off at scale.

**Risk: Platform reliability under peak traffic**
*Impact: High | Likelihood: High (realized on AEM platform)*
The Black Friday outage on the AEM platform demonstrated the consequences of insufficient infrastructure reliability. The new platform had to be validated under peak load conditions before launch.
*Mitigation:* GCS infrastructure was hardened and load-tested ahead of peak retail periods. Uptime monitoring and alerting were implemented prior to go-live.

**Risk: Mobile Core Web Vitals regression**
*Impact: Medium | Likelihood: Low*
A React front-end rebuild risks introducing new performance regressions if components are not optimized for mobile web delivery.
*Mitigation:* Core Web Vitals were benchmarked on the legacy platform and used as a baseline. Performance gates were established as part of the pre-cutover validation checklist for each page group.

**Risk: Content loss or misrepresentation during migration**
*Impact: High | Likelihood: Medium*
With 250+ pages and many contributing stakeholder teams, the risk of content being incorrectly migrated or going unreviewed was significant.
*Mitigation:* Content ownership documentation ensured every page had an assigned reviewer. UAT was completed by content owners prior to each page group cutover.

---

## Dependencies

| Dependency | Owner | Status |
|---|---|---|
| In-house headless CMS — authoring environment ready | Platform Engineering | ✅ Complete |
| GCS infrastructure provisioning and hardening | Infrastructure / DevOps | ✅ Complete |
| React front-end rebuild | Front-End Engineering | ✅ Complete |
| URL restructuring and redirect map (250+ pages) | PM + SEO + Engineering | ✅ Complete |
| Schema metadata implementation | Engineering + SEO | ✅ Complete |
| Page content ownership documentation (all 250+ pages) | PM + Cross-functional | ✅ Complete |
| Stakeholder UAT — Legal, Privacy, Installation, et al. | Lines of Business | ✅ Complete |
| Adobe Target deprecation and personalization migration | Engineering + Marketing | ✅ Complete |

---

## Open Questions & Decisions

| # | Question | Owner | Status |
|---|---|---|---|
| 1 | How should page migration be prioritized across 5 site sections? | PM | ✅ Complete |
| 2 | What schema types are appropriate for each page and content type? | PM + SEO | ✅ Complete |
| 3 | How will personalization segments be mapped from Adobe Target to the new CMS? | PM + Engineering | ✅ Complete |
| 4 | What is the process for stakeholder teams with no prior digital experience to complete UAT? | PM | ✅ Complete |
| 5 | How will SEO performance be monitored post-launch to catch regression early? | PM + SEO | ✅ Complete |

---

## Appendix

### Glossary
- **CMS:** Content Management System — software used to create, manage, and publish digital content
- **Headless CMS:** A CMS architecture where the content repository is decoupled from the presentation layer, connected via API
- **GCS:** Google Cloud Storage — Google's scalable object storage service used for static asset and content delivery
- **LCP:** Largest Contentful Paint — a Core Web Vitals metric measuring perceived page load speed
- **CLS:** Cumulative Layout Shift — a Core Web Vitals metric measuring visual stability during page load
- **Schema metadata:** Structured data markup (e.g. JSON-LD) that helps search engines understand page content and qualify pages for rich search results
- **301 Redirect:** A permanent URL redirect that transfers SEO equity from an old URL to a new one
- **Personalization segment:** A defined audience group used to serve targeted content experiences based on user attributes or behavior
- **UAT:** User Acceptance Testing — validation performed by end users or stakeholders to confirm a system meets requirements before go-live

### Related Documents
- [URL Restructuring and Redirect Map](../seo/redirect-map)
- [Schema Metadata Implementation Guide](../seo/schema-guide)
- [Page Ownership Registry](../governance/page-ownership)
- [Core Web Vitals Benchmark Report](../reports/core-web-vitals)
- [Personalization Migration Spec](../specs/personalization-migration)
