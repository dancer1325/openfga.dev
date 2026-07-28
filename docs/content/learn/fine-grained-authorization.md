---
title: What is Fine-Grained Authorization?
description: Fine-grained authorization decides access at the resource and action level. Learn what FGA is, what it buys you, and how OpenFGA implements it.
sidebar_position: 6
slug: /learn/fine-grained-authorization
---




# What is Fine-Grained Authorization (FGA)?

* FGA
  * == decide access | individual resource & action level
    * != role OR coarse-scope level
      * _Example:_ "Alice is an editor"
    * _Example:_ "Alice can edit document-42" 
    * storing DIRECTLY the graph
  * allows
    * **Per-resource sharing**
      * == user can be granted access -- to -- 1 document
        * WITHOUT inheriting access to everything | workspace
    * **Hierarchical inheritance**
      * == access to a folder -> grants access -- to -- its documents
        * ❌NOT every folder's documents ❌
    * **Reverse queries**
      * == "list EVERY document / this user can read"
      * TODO the query a UI needs to render correctly.
    * **Cross-tenant collaboration.**
      * == Granting 1 resource -- to -- an EXTERNAL user 
        * WITHOUT making them a tenant member

* Coarse-grained models 
  * can simulate -- , with effourt, -- FGA's abilities
    * -- by -- duplicating a graph database | roles tables
 
## How OpenFGA implements FGA?

* [typed model](/docs/configuration-language)
  * defines
    * resource types
    * relations BETWEEN resource types
* [Tuples](/docs/concepts)
  * TODO:record specific relationships between specific principals and specific resources.
* [check API](/docs/interacting/relationship-queries)
  * TODO answers per-action questions in milliseconds.
* [Conditions](/docs/modeling/conditions)
  * TODO cover attribute-driven cases | same model

## FGA use cases 

* **Document management and collaboration** (Google Drive, Notion, Figma patterns).
* **Multi-tenant SaaS** + EXTERNAL sharing
* **AI agents and RAG**
  * EACH user MUST ONLY see their slice of the corpus
    * TODO [AI agent authorization](/docs/use-cases/ai-agent-authorization)
## Choosing the right model

* short decision path
  * [RBAC](/docs/learn/rbac-vs-rebac)
    * TODO use cases
      * Flat access + handful of roles + 1 tenant
  * [ABAC](/docs/learn/abac-vs-rebac) OR [policy engine](/docs/learn/policy-engine)
    * TODO use cases
      * **Decisions driven -- by -- request attributes** (region, department, time-of-day) — start with 
- **Hierarchy, sharing, multi-tenancy, or reverse queries** — you want a relationship engine. OpenFGA handles attribute checks too via [conditions](/docs/modeling/conditions), so you usually don't need a second engine.
- **Mixed infrastructure + application policy** — a policy engine at the admission layer plus OpenFGA for the application is the common pairing.

