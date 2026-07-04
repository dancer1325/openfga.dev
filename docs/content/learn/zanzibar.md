---
title: What is Google Zanzibar?
description: Google Zanzibar is the paper behind Google's global authorization system. Learn what Zanzibar is, what it solved, and how OpenFGA implements it.
sidebar_position: 2
slug: /learn/zanzibar
---

# What is Google Zanzibar?

* [paper](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/)
  * 2019
* == 💡database of **relationship tuples**💡/
  * globally distributed
    * == Google's global authorization system
      * _Example:_ 
        * Drive
        * YouTube
        * Calendar
        * Cloud
  * stores
    * object-relation-user tuples
  * answers 
    * checks
      * _Example:_ user U is related -- , via relation R, to -- object O ?
    * reverse queries -- against the -- resulting graph
      * _Example:_ what objects / type T, user U is related -- , via relation R, to -- ?
* vs OpenFGA
  * OpenFGA
    * open source
      * -> you can use | your data & services
    * 's goal: run | your OWN EXISTING databases
    * NOT follow Spanner-backed architecture
      * Reason:🧠's goal🧠
  * SAME design pattern
  * 
    * 

## What Zanzibar actually is

* == **typed schema** + **tuple store**
  * typed schema OR namespace configuration
    * == types + relations BETWEEN them
  * tuple store
    * indexed -- for --
      * forward queries
      * reverse queries
    * has Zookies
      * == consistency mechanism /
        * lets
          * clients can tie permission checks -- to the -- version of the data / they read

## What Zanzibar solved

* BEFORE Zanzibar,
  * OWN authorization layer / EACH Google product
  * Cross-product features 
    * _Example:_ "share a Drive doc -- to a -- Calendar event guest"
    * -> authorization logic
      * duplicated
      * kept in sync
* Zanzibar
  * enabled Google
    * 1 model
    * 1 store
    * 1 decision surface

## How <ProductName format={ProductNameFormat.ShortForm}/> maps to Zanzibar

* OpenFGA 
  * about Zanzibar core operations
    * == `Write` + `Read` + `Check` + `Expand` + `Watch`
    * implements
    * extends them
      * **Schema**
        * TODO: written in the [<ProductName format={ProductNameFormat.ShortForm}/> DSL](/docs/configuration-language)
      * **Tuples** 
        * stored | PostgreSQL, MySQL, or SQLite
      * **Check** & **Expand**
        * exposed -- via the -- [API](../interacting/relationship-queries)
      * **ListObjects** & **ListUsers**
        * reverse queries that aren't in the Zanzibar paper, for answering *"what can this user see?"* and *"who has access to this object?"*
      * **Conditions** (CEL)
        * <ProductName format={ProductNameFormat.ShortForm}/>'s mechanism for attribute-based decisions, similar in spirit to caveats.
  * 's main benefit
    * design pattern
      * ❌NOT the Google's global infrastructure❌
        * NOT replicated by OpenFGA
        * you can use OpenFGA -- with -- Postgres OR MySQL OR SQLite

* Zanzibar's *model* 
  * the most valuable
    * NOT its operational scale

## Related reading

* [Zanzibar Academy](https://www.zanzibar.academy/)
