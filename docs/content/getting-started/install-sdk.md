---
title: Install SDK Client
sidebar_position: 2
slug: /getting-started/install-sdk
description: Installing SDK client
---

* goal 
  * install the OpenFGA SDK packages

# Install SDK Client

<DocumentationNotice />

* | JS,
  *  [@openfga/sdk](https://www.npmjs.com/package/@openfga/sdk)

```shell
npm install @openfga/sdk
```


```shell
yarn add @openfga/sdk
```
* | Go
  *  [@openfga/go-sdk](https://github.com/openfga/go-sdk)


```
go get -u github.com/openfga/go-sdk
```

```go
import (
    openfga "github.com/openfga/go-sdk"
)

func main() {
    configuration, err := openfga.NewConfiguration(openfga.Configuration{
        ApiUrl:               os.Getenv("FGA_API_URL"), // required, e.g. https://api.fga.example
    })

    if err != nil {
        // .. Handle error
    }
}
```

run

```shell
go mod tidy
```

to update `go.mod` and `go.sum` if you are using them.

</TabItem>
<TabItem value={SupportedLanguage.DOTNET_SDK} label={languageLabelMap.get(SupportedLanguage.DOTNET_SDK)}>

<!-- markdown-link-check-enable -->

The <ProductName format={ProductNameFormat.ShortForm}/> .NET SDK is available on [NuGet](https://www.nuget.org/packages/OpenFga.Sdk).

You can install it using:

- The [dotnet CLI](https://docs.microsoft.com/en-us/nuget/consume-packages/install-use-packages-dotnet-cli):

```powershell
dotnet add package OpenFGA.Sdk
```

- The [Package Manager Console](https://docs.microsoft.com/en-us/nuget/consume-packages/install-use-packages-powershell) inside Visual Studio:

```powershell
Install-Package OpenFGA.Sdk
```

- [Visual Studio](https://docs.microsoft.com/en-us/nuget/consume-packages/install-use-packages-visual-studio), [Visual Studio for Mac](https://docs.microsoft.com/en-us/visualstudio/mac/nuget-walkthrough) and [IntelliJ Rider](https://www.jetbrains.com/help/rider/Using_NuGet.html): Search for and install `OpenFGA.Sdk` in each of their respective package manager UIs.

</TabItem>
<TabItem value={SupportedLanguage.PYTHON_SDK} label={languageLabelMap.get(SupportedLanguage.PYTHON_SDK)}>

The <ProductName format={ProductNameFormat.ShortForm}/> Python SDK is available on [PyPI](https://pypi.org/project/openfga-sdk).

To install:

```
pip3 install openfga_sdk
```

In your code, import the module and use it:

```python
import openfga_sdk
```

</TabItem>
<TabItem value={SupportedLanguage.JAVA_SDK} label={languageLabelMap.get(SupportedLanguage.JAVA_SDK)}>

You can find the Java package on [Maven Central](https://central.sonatype.com/artifact/dev.openfga/openfga-sdk).

Using [Maven](https://maven.apache.org/):

```
<dependency>
    <groupId>dev.openfga</groupId>
    <artifactId>openfga-sdk</artifactId>
    <version>0.3.1</version>
</dependency>
```

Using [Gradle](https://gradle.org/):

```groovy
implementation 'dev.openfga:openfga-sdk:0.3.1'
```

</TabItem>
<TabItem value={SupportedLanguage.CLI} label={languageLabelMap.get(SupportedLanguage.CLI)}>

The <ProductName format={ProductNameFormat.ShortForm}/> CLI is available on [GitHub](https://github.com/openfga/cli).

To install:

### Brew
```shell
brew install openfga/tap/fga
```

### Linux (deb, rpm and apk) packages
Download the .deb, .rpm or .apk packages from the [releases page](https://github.com/openfga/cli/releases).

Debian:
```shell
sudo apt install ./fga_<version>_linux_<arch>.deb
```

Fedora:
```shell
sudo dnf install ./fga_<version>_linux_<arch>.rpm
```

Alpine Linux:
```shell
sudo apk add --allow-untrusted ./fga_<version>_linux_<arch>.apk
```

### Docker
```shell
docker pull openfga/cli; docker run -it openfga/cli
```

### Go

```shell
go install github.com/openfga/cli/cmd/fga@latest
```

### Manually
Download the pre-compiled binaries from the [releases page](https://github.com/openfga/cli/releases).

</TabItem>
</Tabs>

