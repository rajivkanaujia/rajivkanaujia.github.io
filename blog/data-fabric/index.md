---
layout: blog-post
title: "Data Fabric: Revisiting an Old Architecture Discussion"
description: "Revisiting data fabric architecture, metadata, data movement, and access controls for AI applications."
date: 2020-09-01
date_display: "September 2020"
author: Rajiv Kanaujia
tags: [Data Architecture, Data Fabric, AI]
permalink: /blog/data-fabric/
published: true
---

When I wrote about Data Fabric in September 2020, I compared it to 1990s grid computing applied to distributed ETL. That was my first reaction: the terminology was newer than many of the engineering ideas underneath it.

I still think that comparison is useful. We have spent decades connecting systems, moving data, translating formats, and trying to present the result as something coherent. The difficult part has always been what happens when those systems disagree.

The discussion deserves another look, particularly now that we are connecting AI applications to the same information. An answer can read well and still use the wrong definition of a customer, an outdated contract, or information the user should never have received.

## What I Mean by Data Fabric

I use the term to describe an architecture for accessing and managing data across systems. Those systems might include databases, warehouses, object storage, business applications, and document repositories. They do not all have to move into one place.

IBM’s current explanation also treats data fabric as a design approach, with metadata, integration, and governance supporting a unified view of distributed information. That is a useful starting point. [IBM: Data Fabric](https://www.ibm.com/think/topics/data-fabric)

I would then get specific. Suppose sales, billing, and support each have a customer table. Can we explain how their identifiers relate? Does an account mean a company, a subscription, or an individual user? Who decides which record takes precedence?

A common interface can make those tables easier to reach. Someone still has to resolve their meaning. I would want that work visible in the architecture and assigned to people who understand the business.

## A Catalog Is Only the Beginning

It is easy to describe a dataset. Keeping that description useful as the underlying system changes takes considerably more work.

Consider a billing pipeline that changes a column used in a revenue report. I would want to know which reports depend on it, who owns them, and whether yesterday’s successful run tells us anything about today’s output. A diagram created six months ago would provide limited comfort.

OpenLineage is worth looking at here. Its standard records lineage metadata for datasets, jobs, and runs, giving different tools a common way to describe processing relationships. [OpenLineage documentation](https://openlineage.io/docs/)

That helps with tracing dependencies. The response to a failure still needs an owner. I would judge the metadata by whether it helps someone investigate an incorrect result and fix its cause. Collecting more metadata is not much of an achievement on its own.

## Where Mesh and Lakehouse Fit

I find the vocabulary easier to work with when each term answers a different question.

Data mesh puts responsibility with business domains and treats their data as a product. Its principles also include self-service infrastructure and federated governance. Zhamak Dehghani’s explanation makes the organizational responsibilities explicit. [Data Mesh Principles](https://martinfowler.com/articles/data-mesh-principles.html)

A lakehouse combines aspects of lake storage and warehouse analytics. A fabric connects discovery, access, and management across systems. These choices can coexist: domain teams can own data products stored in a lakehouse and exposed through shared services.

Microsoft Fabric adds a naming complication because it is a particular product platform. I would separate evaluation of that product from agreement on the architecture. Otherwise, a discussion about responsibilities can turn into a discussion about features before the requirements are understood.

## Be Precise About Data Movement

There are better options today for accessing information without building a separate copy for every consumer. The details matter, though.

Microsoft’s July 2026 OneLake documentation distinguishes shortcuts, which reference data, from mirroring, which can reference or replicate it depending on the source. It also describes situations where transformations and orchestration still need data movement tools. [Shortcuts and Mirroring](https://learn.microsoft.com/en-us/fabric/onelake/unify-data)

I would ask what happens when the source becomes unavailable. Does a report fail, use cached information, or return partial results? What does repeated access cost? If data is replicated, how far behind can it fall?

Apache Iceberg offers another useful improvement: schema and partition evolution. Partition specifications can change without immediately rewriting existing files. That gives engineers room to adapt storage layouts as workloads change. [Apache Iceberg: Evolution](https://iceberg.apache.org/docs/latest/evolution/)

These capabilities solve real problems. Their value should be explained through the specific work they eliminate and the dependencies they leave behind.

## AI Brings Permissions Into the Query

Imagine an assistant answering a question about an upcoming renewal. It retrieves a contract, several support cases, and an internal pricing exception. All three may be relevant. They may also have different access restrictions.

The application needs to carry authorization through ingestion, indexing, and retrieval. A good answer cannot compensate for exposing a document to the wrong person.

Azure AI Search’s documentation illustrates the implementation details involved. It distinguishes security filters from native identity and sensitivity-label capabilities that remain in preview, and notes that permission changes can take time to synchronize. [Document-Level Access Control](https://learn.microsoft.com/en-us/azure/search/search-document-level-access-overview)

I would explicitly test what happens after access is revoked. Does the indexed copy retain old permissions? Can a cached response still expose the content? Those questions belong in the initial design.

## Where I Would Start

Choose one business question. The renewal example is sufficient: which accounts need attention, and why? Identify the sources, settle the definitions, assign ownership, and agree on how fresh the answer needs to be.

Then measure the effort required to get a usable answer. Track access delays, failed refreshes, duplicate pipelines, investigation time, and operating cost. Add another source when there is a reason to do so.

For a smaller organization, this may be a modest implementation using existing tools. I would resist introducing a new service unless someone can explain who will maintain it, how failures will be detected, and what improvement the business can reasonably expect from the investment.

My original comparison with distributed computing still stands. What I would emphasize more today is the ongoing responsibility for meaning, permissions, and change. A data fabric is useful when it makes that responsibility easier to carry. That is what I would look for before committing to a platform.
