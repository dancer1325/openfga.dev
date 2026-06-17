---
id: overview
title: 'Getting Started'
slug: /getting-started
sidebar_position: 0
description: 'OpenFGA tutorial and quickstart: install the server, configure an authorization model, write tuples, and run your first permission checks in minutes.'
---

* goal
  * step-by-step guide -- to -- 
    * install OpenFGA
      * [setup OpenFGA server](setup-openfga/overview.md)
      * [install SDK client](install-sdk.md)
      * [create an OpenFGA store / owns an authorization model + relationship tuples](create-store.md)
    * [configure the SDK client -- for -- your store](setup-sdk-client.md)
    * [configure an authorization model](configure-model.md)
    * [update relationship tuples](update-tuples.md)
    * [run permission checks](perform-check.md)

TODO:
      
      
      { '@type': 'HowToStep', position: 7, name: 'Perform a Check', text: 'Programmatically perform an authorization check against an OpenFGA store.', url: 'https://openfga.dev/docs/getting-started/perform-check' },
      { '@type': 'HowToStep', position: 8, name: 'Perform a List Objects Request', text: 'Programmatically perform a list objects request against an OpenFGA store.', url: 'https://openfga.dev/docs/getting-started/perform-list-objects' },
      { '@type': 'HowToStep', position: 9, name: 'Integrate Within a Framework', text: 'Integrate authorization checks with a framework.', url: 'https://openfga.dev/docs/getting-started/framework' },
    ],
};


# Content

<CardGrid
  middle={[
    {
      title: 'Setup OpenFGA',
      description: 'How to setup an OpenFGA server.',
      to: 'getting-started/setup-openfga/overview',
    },
    {
      title: 'Install SDK Client',
      description: 'Install the SDK for the language of your choice.',
      to: 'getting-started/install-sdk',
    },
    {
      title: 'Create a Store',
      description: 'Creating an OpenFGA entity that owns an authorization model and relationship tuples.',
      to: 'getting-started/create-store',
    },
    {
      title: 'Setup SDK Client for Store',
      description: 'Configure the SDK client for your store.',
      to: 'getting-started/setup-sdk-client',
    },
    {
      title: 'Configure Authorization Model',
      description: 'Programmatically configure authorization model for an {ProductName} store.',
      to: 'getting-started/configure-model',
    },
    {
      title: 'Update Relationship Tuples',
      description: 'Programmatically write authorization data to an {ProductName} store.',
      to: 'getting-started/update-tuples',
    },
    {
      title: 'Perform a Check',
      description: 'Programmatically perform an authorization check against an {ProductName} store.',
      to: 'getting-started/perform-check',
    },
    {
      title: 'Perform a List Objects Request',
      description: 'Programmatically perform a list objects request against an {ProductName} store.',
      to: 'getting-started/perform-list-objects',
    },
    {
      title: 'Integrate Within a Framework',
      description: 'Integrate authorization checks with a framework.',
      to: 'getting-started/framework',
    },
    {
      title: 'Immutable Authorization Models',
      description: 'Learn how to take advantage of the immutable properties of Authorization Models in {ProductName}.',
      to: 'getting-started/immutable-models',
    },
    {
      title: 'Best Practices',
      description: 'Best Practices for implementing OpenFGA.',
      to: '../docs/best-practices',
    }
  ]}
/>
