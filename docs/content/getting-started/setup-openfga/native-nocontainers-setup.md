---
title: Native Setup Guide (No Containers)
description: Setting up an OpenFGA server without containers using Homebrew, precompiled binaries, or building from source
sidebar_position: 3
slug: /getting-started/setup-openfga/native
---

# Setup OpenFGA without Containers

This guide covers how to install and run OpenFGA directly on your machine without Docker or Kubernetes.

## Homebrew

If you are a [Homebrew](https://brew.sh/) user, you can install [OpenFGA](https://formulae.brew.sh/formula/openfga) with:

```shell
brew install openfga
```

Then run:

```shell
openfga run
```

## Precompiled Binaries

Download your platform's [latest release](https://github.com/openfga/openfga/releases/latest) and extract it. Then run:

```shell
./openfga run
```

## Build from Source

> **Note:** Make sure you have the latest version of Go installed. See the [Go downloads](https://go.dev/dl/) page.

### Using `go install`

```shell
export PATH=$PATH:$(go env GOBIN) # make sure $GOBIN is on your $PATH
go install github.com/openfga/openfga/cmd/openfga
openfga run
```

### Using `go build`

```shell
git clone https://github.com/openfga/openfga.git && cd openfga
go build -o ./openfga ./cmd/openfga
./openfga run
```

## Verify Installation

Test your installation by creating a store:

```shell
curl -X POST 'localhost:8080/stores' \
  --header 'Content-Type: application/json' \
  --data-raw '{"name": "openfga-demo"}'
```

If everything is running correctly, you should get a response like:

```json
{
  "id": "01G3EMTKQRKJ93PFVDA1SJHWD2",
  "name": "openfga-demo",
  "created_at": "2022-05-19T17:11:12.888680Z",
  "updated_at": "2022-05-19T17:11:12.888680Z"
}
```
