# PRD: E-Commerce CMS Platform Migration
### Home Improvement Retailer — AEM to In-House Headless CMS on Google Cloud

---

## Overview

This repository contains the Product Requirements Document for the migration of a large home improvement retailer's e-commerce web platform — 250+ landing pages spanning shop, savings, installation, help, and brand content — from Adobe Experience Manager (AEM) to an in-house headless CMS with a React front end hosted on Google Cloud Storage.

The migration was elevated to a business-critical priority after a Black Friday outage on the legacy AEM platform. The project was completed in approximately 18 months, with all success metrics achieved.

📄 **[Read the full PRD →](./prd-ecommerce-cms-migration.md)**

---

## What This Demonstrates

**Crisis-driven prioritization** — The Black Friday outage is documented as the event that elevated this migration from a roadmap item to a business-critical initiative. The PRD shows how I framed the business case and scoped the response — not just reacting to the incident, but using it to drive alignment on a platform overhaul that addressed root causes rather than symptoms.

**SEO-first migration strategy** — Restructuring 250+ pages from a flat single-subdirectory URL structure into 5 logical subdirectories, with full redirect mapping and schema metadata implementation, required treating SEO continuity as a first-class technical requirement rather than a post-launch concern. Zero loss of indexed pages post-migration is a tracked and achieved success metric.

**Cross-functional stakeholder coordination at scale** — Many contributing teams — Legal, Privacy, Installation Services — had no prior relationship with the digital organization. The PRD documents how page content ownership was formally established across all 250+ pages as a parallel workstream, enabling UAT at scale without the project grinding to a halt on content review bottlenecks.

**Completed project with fully realized outcomes** — Unlike in-progress platform migrations, this PRD reflects a completed project. All success metrics are marked ✅ Achieved — reliability, Core Web Vitals, SEO restructuring, dual-authoring elimination, cloud migration, and content ownership governance. This demonstrates the full arc from problem statement through delivery.

**Architectural decision: cloud migration as a strategic objective** — The decision to migrate to Google Cloud Storage is documented as both a technical necessity (reliability) and an organizational strategic priority (cloud modernization, infrastructure cost reduction). The PRD reflects how PM judgment connects platform decisions to business context, not just engineering preference.

---

## Document Metadata

| | |
|---|---|
| **Product** | E-Commerce Web Platform |
| **Document Type** | Platform PRD |
| **Status** | Completed |
| **Timeline** | ~18 months · Late 2019 – Mid 2021 |
| **Stack** | In-house headless CMS · React · Google Cloud Storage |

---

## Related Artifacts

| Artifact | Description |
|---|---|
| [PRD: Enterprise CMS Platform Migration](https://github.com/thedmons/prd-cms-platform-migration) | Related platform migration PRD — different domain (fintech vs. e-commerce), similar migration pattern |
