---
id: overview
title: 'Interacting with the API'
slug: /interacting
sidebar_position: 0
description: Programmatically writing authorization related data and interact with the API
---

* goal
  * how to programmatically write authorization -- related data to -- OpenFGA 

* helps you
  * integrate OpenFGA -- with -- your system
 
* requirements 
  * authorization model 

# Content

<CardGrid
  bottom={[
    {
      title: 'Manage User Access',
      description: "Write relationship tuples to manage a user's access to an object.",
      to: 'interacting/managing-user-access',
    },
    {
      title: 'Manage Group Access',
      description: 'Write relationship tuples to manage access to an object for all members of a group.',
      to: 'interacting/managing-group-access',
    },
    {
      title: 'Manage Group Membership',
      description: 'Write relationship tuples to manage the users that are members of a group.',
      to: 'interacting/managing-group-membership',
    },
    {
      title: 'Manage Relationships Between Object',
      description:
        'Write relationship tuples to manage how two objects are related. E.g. parent folder and child document.',
      to: 'interacting/managing-relationships-between-objects',
    },
    {
      title: 'Relationship Queries',
      description: 'An overview of how to use the Check, Read, Expand, and ListObject APIs.',
      to: 'interacting/relationship-queries',
    },
    {
      title: 'Search with Permissions',
      description: 'Implementing search with OpenFGA.',
      to: 'interacting/search-with-permissions',
    },
]}
/>
