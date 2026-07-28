---
title: ABAC vs ReBAC
description: ABAC decides on attributes; ReBAC decides on relationships. Learn which fits which problem — and how OpenFGA covers both via conditions.
sidebar_position: 5
slug: /learn/abac-vs-rebac
---

# ABAC vs. ReBAC

* **Attribute-Based Access Control (ABAC)**
  * *"role = engineer AND region = EU"*

* **Relationship-Based Access Control (ReBAC)**
  * _Example:_ user is editor of doc / is | folder / shared with team

|                                 | ABAC                                                                   | ReBAC                            |
|---------------------------------|------------------------------------------------------------------------|----------------------------------|
| Source of truth                 | request's attributes & resource's attributes & principal's attributes  | Stored relationship tuples       |
| Ergonomics for hierarchy        | Needs explicit attribute lookups                                       | Native                           |
| Ergonomics for attribute checks | Native                                                                 | Needs conditions/contextual data |
| Reverse queries                 | Hard — must enumerate resources                                        | First-class                      |
| Common engines                  | OPA (Rego), Cedar, AWS IAM                                             | SpiceDB, Ory Keto                |

## When ABAC fits

- The decision is **stateless from the engine's perspective** — everything needed is on the request: claims, headers, resource metadata.
- Rules involve **comparisons** (`amount < limit`, `region = EU`, `time within business_hours`).
- You want policies versioned in Git as code or YAML, not stored as data.

## When ReBAC fits

- The decision depends on **relationships that change at write time** — membership, sharing, hierarchy.
- You need **reverse queries** for UI rendering or filtered listings.
- Permissions need to traverse multi-hop graphs (team → project → folder → document).

## OpenFGA does both

OpenFGA is a ReBAC engine, but it covers ABAC needs through [conditions](/docs/modeling/conditions) (CEL expressions evaluated at check time) and [contextual tuples](/docs/interacting/contextual-tuples) (request-time data passed into the check). For most applications that's enough — you don't need a second engine.

## When you might want both

If you also need policy outside the application — Kubernetes admission, Terraform validation, service-mesh request rules — pair OpenFGA with a [policy engine](/docs/learn/policy-engine) like OPA. OpenFGA inside the app, OPA at the infrastructure layer.

## Related reading

<RelatedSection
  description="Learn more about {ProductName}."
  relatedLinks={[
    {
      title: 'ReBAC overview',
      description: 'Relationship-Based Access Control explained.',
      link: './rebac',
      id: './rebac',
    },
    {
      title: 'RBAC vs. ReBAC',
      description: 'How roles and relationships compare.',
      link: './rbac-vs-rebac',
      id: './rbac-vs-rebac',
    },
    {
      title: 'Conditions',
      description: 'Attribute-based decisions in {ProductName}.',
      link: '../modeling/conditions',
      id: '../modeling/conditions',
    },
  ]}
/>
