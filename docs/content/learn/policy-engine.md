p---
title: Policy Engines vs Relationship Engines
description: Policy engines like OPA and Cedar evaluate rules over data. Relationship engines like OpenFGA store and query the graph. Here's when to use which.
sidebar_position: 7
slug: /learn/policy-engine
---

# Policy Engines vs. Relationship Engines

* authorization toolbox
  * **Policy engines**
    * == OPA (Rego) + Cedar
    * evaluate: policies / DSL format vs input data / passed | EACH request
    * **stateless**
      * == you supply the data
  * **Relationship engines**
    * [Zanzibar](/docs/learn/zanzibar) tradition
    * _Examples:_ SpiceDB, Ory Keto
    * store relationship tuples | database
    * answer queries | stored graph

* engine
  * == database

## How to choose the policy engine

* -- based on the -- attribute
  * are
    * claims
    * resource metadata
    * request context
  * AVAILABLE | request time  
    * -> engine does NOT need to fetch anything 

TODO: You **already run one** for infrastructure or admission policy — extending it to cover application rules avoids a second decision surface.

* OPA
  * default choice
    * Reason: OPA's [graduated CNCF status](https://www.cncf.io/projects/open-policy-agent-opa/) 

## When a relationship engine fits

* Decisions 
  * -- depend on -- relationships / change | write time
    * — group membership, document sharing, folder hierarchy, multi-tenant ownership
- The data behind the decision is **too large or too dynamic to ship on every request** — millions of memberships, deeply nested hierarchies — so the engine needs to own the store.
- You need **reverse queries** — *"list every resource this user can read"* — which inherently require a stored graph.
- Permissions are **per-resource and per-user**, not just per-attribute.

## Policy as code in <ProductName format={ProductNameFormat.ShortForm}/>

The "policy in Git, reviewed via PR" workflow isn't unique to policy engines. The <ProductName format={ProductNameFormat.ShortForm}/> [model DSL](/docs/configuration-language) is the policy: types, relations, and [conditions](/docs/modeling/conditions) live in a text file you commit, review, and deploy like any other code. The same model backs authorization decisions across services, languages, and domains — one source of truth instead of policy logic re-implemented per service.

## You can use both

Pairing them is common: a relationship engine for application authorization, a policy engine at the infrastructure or admission layer. Inside the application, <ProductName format={ProductNameFormat.ShortForm}/> covers most attribute-driven rules with [conditions](/docs/modeling/conditions) and [contextual tuples](/docs/interacting/contextual-tuples), so a second engine isn't always needed.

## Related reading

<RelatedSection
  description="Learn more about {ProductName}."
  relatedLinks={[
    {
      title: 'ABAC vs. ReBAC',
      description: 'Attributes vs. relationships — and how they combine.',
      link: './abac-vs-rebac',
      id: './abac-vs-rebac',
    },
  ]}
/>
