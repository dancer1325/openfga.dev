---
title: Concepts
sidebar_position: 2
slug: /concepts
description: Learning about FGA concepts
---

# Concepts

* OpenFGA service
  * TODO: answers <IntroductionSection linkName="authorization" section="authentication-and-authorization"/> [checks](#what-is-a-check-request) by determining whether a **[relationship](#what-is-a-relation)** exists between an [object](#what-is-an-object) and a [user](#what-is-a-user)
* Checks reference your **[authorization model](#what-is-an-authorization-model)** against your **[relationship tuples](#what-is-a-relationship-tuple)** for authorization authority

## What Is A Type?

* == string
* == class of objects / SIMILAR characteristics
* _Examples:_ 
  * `workspace`
  * `repository`
  * `organization`
  * `document`

## What Is A Type Definition?

* **type definition**
  * == ALL possible relations a user OR another object can have -- in relation to -- this type

## What Is An Authorization Model?

* **authorization model**
  * \>= 1 type definitions
  * uses
    * define the system's permission model
  * ways to define it (== syntaxes)
    * JSON syntax / accepted by the OpenFGA API + follows the [Zanzibar original syntax](https://research.google/pubs/pub48190/)
      * [MORE](./configuration-language.md#equivalent-zanzibar-concepts)
    * DSL / accepted by [OpenFGA VS Code extension](https://marketplace.visualstudio.com/items?itemName=openfga.openfga-vscode) + [OpenFGA CLI](https://github.com/openfga/cli/)
      * _Example:_ [Sample Stores](https://github.com/openfga/sample-stores)  
      * uses
        * BEFORE sent to the API, translated to API-supported syntax -- via -- 
          * CLI OR
          * [OpenFGA language](https://github.com/openfga/language) 

* way to determine whether a [relationship](#what-is-a-relationship) exists BETWEEN a [user](#what-is-a-user)  -- & -- [object](#what-is-an-object) -- depends on -- 
  * [relationship tuples](#what-is-a-relationship-tuple)
  * authorization model

## What Is A Store?

* **store**
  * == OpenFGA's entity /
    * organize authorization check data
  * == >=1 versions of an [authorization model](#what-is-an-authorization-model) + >=1 [relationship tuples](#what-is-a-relationship-tuple) (OPTIONAL)
  * 👀recommendations: store ALL data / may be related OR affect your authorization result | 1! store👀
    * Reason:🧠store's data can NOT be shared -- ACROSS -- stores🧠 
  * you can create SEPARATE stores / EACH authorization needs OR isolated environments

## What Is An Object?

* **object**
  * == entity | system
  * == [type](#what-is-a-type) + identifier

+ _Example:_[here](./modeling/direct-access.md)
  + `workspace:fb83c013-3060-41f4-9590-d3233a67938f`
  + `repository:auth0/express-jwt`
  + `organization:org_ajUc9kJ`
  + `document:new-roadmap`

## What Is A User?

* **user**
  * == entity | system /
    * can be related -- to an -- object
  * == [type](#what-is-a-type) + identifier + relation (OPTIONAL)

* _Example:_
  * -- as -- identifier
    * `user:anne`
    * `user:4179af14-f0c0-4930-88fd-5570c7bf6f59`
  * -- as -- any object
    * `workspace:fb83c013-3060-41f4-9590-d3233a67938f`
    * `repository:auth0/express-jwt`
    * `organization:org_ajUc9kJ`
  * -- as -- **userset**
    * == group OR set of users
    * `organization:org_ajUc9kJ#members`
      * == set of users / related -- , as `member`, to the -- object `organization:org_ajUc9kJ`
  * -- as -- everyone
    * `*`

* [more](./modeling/direct-access.md)

## What Is A Relation?

* **relation**
  * == string / defined | authorization model's type definition 
  * == possible relationship BETWEEN an object ('s type defined | type definition) -- & a -- user | system
  * _Examples:_
    * user can be a 
      * `reader` of a document
      * `member` of a team 
    * Team can `administer` a repo

## What Is A Relation Definition?

* **relation definition**
  * == conditions / relationship is possible
    * _Example:_ `editor /` describe a possible relationship BETWEEN a user & object | `document` type, allows
      * **user identifier to object relationship**
        * the user id `anne` of type `user` is related to the object `document:roadmap` as `editor`
      * **object to object relationship**
        * object `application:ifft` is related to the object `document:roadmap` as `editor`
      * **userset to object relationship**
        * the userset `organization:auth0.com#member` is related to `document:roadmap` as `editor`
        * indicates that the set of users who are related to the object `organization:auth0.com` as `member` are related to the object `document:roadmap` as `editor`s
        * allows for potential solutions to use-cases like sharing a document internally with all members of a company or a team
      * **everyone to object relationship**
        * everyone (`*`) is related to `document:roadmap` as `editor`
        * this is how one could model publicly editable documents

* defined | [authorization model](#what-is-an-authorization-model)

## What Is A Directly Related User Type?

* **directly related user type**
  * == [] / 
    * specified | type definition
    * == types of users / can be DIRECTLY -- related to -- that relation

TODO: 
A relationship tuple with user `user:anne` or `user:3f7768e0-4fa7-4e93-8417-4da68ce1846c`
may be written for objects with type `document` and relation `viewer`, 
so writing `{"user": "user:anne","relation":"viewer","object":"document:roadmap"}` succeeds.
A relationship tuple with a disallowed user type for the `viewer` relation 
on objects of type `document` - for example `workspace:auth0` or `folder:planning#editor`
will be rejected, so writing `{"user": "folder:product","relation":"viewer","object":"document:roadmap"}` will fail.
This affects only relations that are [directly related](#what-are-direct-and-implied-relationships) and have [direct relationship type restrictions](./configuration-language.mdx#direct-relationship-type-restrictions)
in their relation definition.

## What is a Condition?

* **condition**
  * == `function(>=1 parameter) {expression}`
    * return: boolean
    * `expression`
      * defined -- by -- using [Google's Common Expression Language (CEL)](https://github.com/google/cel-spec)

## What Is A Relationship Tuple?

* **relationship tuple**
  * == base tuple/triplet /
    * == [user](#what-is-a-user) + [relation](#what-is-a-relation) + [object](#what-is-an-object) + [condition](#what-is-a-condition)
    * condition
      * OPTIONAL
    * written & stored | OpenFGA

## What Is A Conditional Relationship Tuple?

* **conditional relationship tuple** 
  * == [relationship tuple](#what-is-a-relationship-tuple) /
    * [relationship](#what-is-a-relationship) is represented -- based on -- a [condition](#what-is-a-condition)

## What Is A Relationship?

* **relationship** 
  * == realization of a relation BETWEEN a user -- & -- an object
    * determined -- based on -- user + object
  * [types](#what-are-direct-and-implied-relationships)
    * direct
    * implied

## What Are Direct And Implied Relationships?

* **direct relationship** (R) BETWEEN user X -- & -- object Y 
  * == relationship tuple (user=X, relation=R, object=Y) EXIST & 's authorization model allows the direct relationship
-- because of -- [direct relationship type restrictions](./configuration-language.mdx#direct-relationship-type-restrictions)

* **implied (or computed) relationship** (R) exists BETWEEN user X -- & -- object Y 
  * == user X is related -- to an -- object Z 
/ is in a direct or implied relationship -- with -- object Y & and 's authorization model
allows it

- `user:anne` has a direct relationship with `document:new-roadmap` as `viewer` if the [type definition](#what-is-a-type-definition) 
allows it with [direct relationship type restrictions](./configuration-language.mdx#direct-relationship-type-restrictions), and one of the following [relationship tuples](#what-is-a-relationship-tuple) exist:

  - <RelationshipTuplesViewer
      relationshipTuples={[
        {
          _description: 'Anne of type user is directly related to the document',
          user: 'user:anne',
          relation: 'viewer',
          object: 'document:new-roadmap',
        },
      ]}
    />

  - <RelationshipTuplesViewer
      relationshipTuples={[
        {
          _description: 'Everyone (`*`) of type user is directly related to the document',
          user: 'user:*',
          relation: 'viewer',
          object: 'document:new-roadmap',
        },
      ]}
    />

  - <RelationshipTuplesViewer
      relationshipTuples={[
        {
          _description: 'The userset is directly related to this document',
          user: 'team:product#member',
          relation: 'viewer',
          object: 'document:new-roadmap',
        },
        {
          _description: 'AND Anne of type user is a member of the userset team:product#member',
          user: 'user:anne',
          relation: 'member',
          object: 'team:product',
        },
      ]}
    />

- `user:anne` has an **implied relationship** with `document:new-roadmap` as `viewer` if the type definition allows it, and the presence of relationship tuples satisfying the relationship exist.

  For example, assume the following type definition:

  <AuthzModelSnippetViewer
    configuration={{
      schema_version: '1.1',
      type_definitions: [
        {
          type: 'document',
          relations: {
            viewer: {
              union: {
                child: [
                  {
                    // a user can be assigned a direct `viewer` relation, i.e., not implied through another relation
                    this: {},
                  },
                  {
                    // a user who is related as an editor is also implicitly related as a viewer
                    computedUserset: {
                      relation: 'editor',
                    },
                  },
                ],
              },
            },
            editor: {
              this: {},
            },
          },
          metadata: {
            relations: {
              editor: { directly_related_user_types: [{ type: 'user' }] },
              viewer: { directly_related_user_types: [{ type: 'user' }] },
            },
          },
        },
      ],
    }} skipVersion={true}
  />

  And assume the following relationship tuple exists in the system:

  <RelationshipTuplesViewer
    relationshipTuples={[
      {
        user: 'user:anne',
        relation: 'editor',
        object: 'document:new-roadmap',
      },
    ]}
  />

  In this case, the [relationship](#what-is-a-relationship) between `user:anne` and `document:new-roadmap` as a `viewer` is implied from the direct `editor` relationship `user:anne` has with that same document. Thus, the following request to [check](#what-is-a-check-request) whether a viewer relationship exists between `user:anne` and `document:new-roadmap` will return `true`.

  <CheckRequestViewer user={'user:anne'} relation={'viewer'} object={'document:new-roadmap'} allowed={true} />

</details>

<details>
<summary>

## What Is A Check Request?

* **check request** 
  * == call -- to the -- <ProductName format={ProductNameFormat.LongForm}/> check endpoint
    * return whether the user has a certain relationship with an object
    * | SDK,

</summary>

Check requests use the `check` methods in the <ProductName format={ProductNameFormat.ShortForm}/> SDKs ([JavaScript SDK](https://www.npmjs.com/package/@openfga/sdk)/[Go SDK](https://github.com/openfga/go-sdk)/[.NET SDK](https://www.nuget.org/packages/OpenFga.Sdk)) by manually calling the [check endpoint](/api/service#Relationship%20Queries/Check) using curl or in your code. The check endpoint responds with `{ "allowed": true }` if a relationship exists, and with `{ "allowed": false }` if the relationship does not.

For example, the following will check whether `anne` of type user has a `viewer` relation to `document:new-roadmap`:

<CheckRequestViewer user={'user:anne'} relation={'viewer'} object={'document:new-roadmap'} allowed={true} />

For more information, see the [Relationship Queries page](./interacting/relationship-queries.mdx) and the official [Check API Reference](/api/service#Relationship%20Queries/Check).

</details>

<details>
<summary>

## What Is A List Objects Request?

* **list objects request** 
  * == call -- to the -- OpenFGA's list objects endpoint / returns ALL objects / given type / user has a specified relationship with
    * completed using the `listobjects` methods in the <ProductName format={ProductNameFormat.ShortForm}/> SDKs ([JavaScript SDK](https://www.npmjs.com/package/@openfga/sdk)/[Go SDK](https://github.com/openfga/go-sdk)/[.NET SDK](https://www.nuget.org/packages/OpenFga.Sdk)) by manually calling the [list objects endpoint](/api/service#Relationship%20Queries/ListObjects) using curl or in your code.

The list objects endpoint responds with a list of objects for a given type that the user has the specified relationship with.

For example, the following returns all the objects with document type for which `anne` of type user has a `viewer` relation with:

<ListObjectsRequestViewer
  authorizationModelId="01HVMMBCMGZNT3SED4Z17ECXCA"
  objectType="document"
  relation="viewer"
  user="user:anne"
  expectedResults={['document:otherdoc', 'document:planning']}
/>

[Relationship Queries page](./interacting/relationship-queries.mdx)
 [List Objects API Reference](/api/service#Relationship%20Queries/ListObjects).

</details>
<details>
<summary>

## What Is A List Users Request?

* **list users request**
  * == call -- to the -- OpenFGA list users endpoint /
    * returns ALL users of a given type / have a specified relationship -- with an -- object
  * completed | use
    * SDK's `ListUsers`
    * `fga query list-users`
    * calling the [ListUsers endpoint](/api/service#Relationship%20Queries/ListUsers)

For example, the following returns all the users of type `user` that have the `viewer` relationship for `document:planning`:

<ListUsersRequestViewer
  authorizationModelId="01HVMMBCMGZNT3SED4Z17ECXCA"
  objectType="document"
  objectId="planning"
  relation="viewer"
  userFilterType="user"
  expectedResults={{
    users: [
      { object: { type: "user", id: "anne" }}, 
      { object: { type: "user", id: "beth" }}
    ]
  }}
/>

* [ListUsers API Reference](/api/service#Relationship%20Queries/ListUsers)

</details>
<details>
<summary>

## What Are Contextual Tuples?

* contextual tuples
  * == tuples /
    * can be added | 
      * Check request
      * ListObjects request
      * ListUsers request
      * Expand request
    * ONLY exist | particular request's context
    * NOT persisted | datastore
  * vs contextual tuples 
    * == user, relation and object. Unlike relationship tuples, they are not written to the store. However, if contextual tuples are sent alongside a check request in the context of a particular check request, they are treated if they had been written in the store.

<!-- markdown-link-check-disable -->

* [Contextual and Time-Based Authorization](./modeling/contextual-time-based-authorization.mdx), [Authorization Through Organization Context](./modeling/organization-context-authorization.mdx)
* [Check API Request Documentation](/api/service#Relationship%20Queries/Check)

<!-- markdown-link-check-enable -->

</details>

<details>
<summary>

## What Is Type Bound Public Access?

* `<type>:*`
  * == every object of [type] | being invoked -- as a -- user | relationship tuple
* == special syntax 
For example, `user:*` represents every object of type `user` , including those not currently present in the system.

</summary>

For example, to indicate `document:new-roadmap` is publicly writable (in other words, has everyone of type `user` as an editor, add the following [relationship tuple](#what-is-a-relationship-tuple):

<RelationshipTuplesViewer
  relationshipTuples={[
    {
      user: 'user:*',
      relation: 'editor',
      object: 'document:new-roadmap',
    },
  ]}
/>

Note: `<type>:*` cannot be used in the `relation` or `object` properties. In addition, `<type>:*` cannot be used as part of a userset in the tuple's user field.
For more information, see [Modeling Public Access](./modeling/public-access.mdx) and [Advanced Modeling: Modeling Google Drive](./modeling/advanced/gdrive.mdx).

</details>
