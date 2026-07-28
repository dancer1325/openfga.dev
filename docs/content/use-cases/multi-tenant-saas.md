---
title: Multi-Tenant SaaS Authorization with OpenFGA
description: Authorize multi-tenant SaaS applications with OpenFGA. Strict tenant isolation, shared infrastructure, and cross-tenant sharing where you want it.
sidebar_position: 5
slug: /use-cases/multi-tenant-saas
---


# Multi-Tenant SaaS Authorization

* Multi-tenant SaaS
  * == one of OpenFGA's MOST common production shapes
  * SAME binary serves EVERY tenant
    * tenant boundaries are enforced 
      * | the authorization model
      * ❌NOT | database OR service layer❌

## The pattern

* `organization` OR `tenant`
  * ALL OTHER resources belong to it
    *
- `organization` has members, admins, and owners.
- `workspace`, `project`, and `document` types each declare a `parent` relation pointing at an `organization`.
- Relations like `can_view` and `can_edit` traverse the parent edge so organization membership grants the right access automatically.

This gives you:

- **Hard tenant isolation by default.** A user only has tuples for the organizations they belong to, so list-objects naturally returns nothing cross-tenant.
- **Cross-tenant sharing when you want it.** A document can also have individually granted users from other organizations — same model, no special case.
- **A single store for all tenants.** Operationally cheaper than per-tenant databases; the tuple count grows linearly with usage rather than fan-out.

## Per-tenant custom roles

Most SaaS products eventually need tenant-defined roles — *"Acme wants a `billing-manager` role; Globex wants a `compliance-reviewer` role"* — without redeploying the model. The pattern is to make `role` a first-class type whose `assignee` relation can be a user, another role, or a group, and then bind those roles to organization-level permissions:

```dsl.openfga
type user

type group
  relations
    define member: [user, group#member]

type role
  relations
    define assignee: [user, role#assignee, group#member]

type organization
  relations
    define admin: [user, role#assignee]
    define billing_manager: [role#assignee] or admin
    define document_manager: [role#assignee] or admin

    define can_invite_user: admin
    define can_edit_billing: billing_manager
    define can_create_document: document_manager

type document
  relations
    define organization: [organization]
    define editor: document_manager from organization
    define viewer: document_manager from organization

    define can_view: viewer or editor
    define can_edit: editor
```

Each tenant creates its own `role:acme-billing-manager`, `role:acme-document-management`, etc., and binds them to the predefined organization-level relations (`billing_manager`, `document_manager`, `admin`). Users or groups become assignees of those roles, and document-level permissions inherit through the organization. The model itself stays static; tenants get full flexibility on which roles exist and who is in them.

The full working example — including tuples, group nesting (`group:acme-data-engineering#member` ∈ `group:engineering#member`), and `list_users` assertions — is in the [multitenant-rbac sample store](https://github.com/openfga/sample-stores/tree/main/stores/multitenant-rbac). You can run it locally with the [FGA CLI](/docs/getting-started/cli) to see the checks pass.

## Modeling building blocks

- [Modeling parent-child](/docs/modeling/parent-child)
- [Modeling roles](/docs/best-practices/modeling-roles)
- [Source of truth](/docs/best-practices/source-of-truth)

## Related reading

- [Microservices authorization](/docs/use-cases/microservices-authorization)
