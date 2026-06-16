# OpenFGA Documentation

* -- based on -- [Docusaurus](https://docusaurus.io/)

## Getting Started

### Setup and Installation

#### Clone the repo locally

Run `git clone https://github.com/openfga/openfga.dev.git` to clone the repo to your machine.

#### Setup Git LFS (Large File Storage)

* Follow the instructions [here](https://git-lfs.github.com/) to install git lfs on your system.
* If you haven't done so yet, run `git lfs install` to set up git lfs for your account.
* Run `git lfs pull`
* Run `git lfs checkout`

Currently `mp4`, `webm` and `svg` files are tracked
* If you need to track more media formats, run: `git lfs track "*.extension"`

#### Install Dependencies

To run the docs locally you will need to first install dependencies:

```
npm install
```

#### Running in Development

You can then run 

```
npm run dev
```

This command starts a local development server and opens up a browser window
* Most changes are reflected live without having to restart the server.

#### Building for Production

To generate a production build

##### NPM
`npm run build` # Generated files will be in the ./build directory

To launch a server with the build files, run 

```
npm run serve
```

<!-- markdown-link-check-disable -->
You will then be able to browse the documentation at http://localhost:3000/   
<!-- markdown-link-check-enable-->

#### Docker


##### Build

To build in development mode

```
docker build --target development . -t fga-docs-dev
```

To run in development mode

```
docker run --init --rm -p 3000:3000 fga-docs-dev
```

The generated webpages will be available in http://localhost:3000.

##### Production

To build in production mode


```
docker build . -t fga-docs
```

Run

```
docker run --init --rm -p 3000:80 fga-docs
```

## PR Preview
GitHub Action [Deploy PR Preview](https://github.com/marketplace/actions/deploy-pr-preview) allows previewing of proposed changes. The URL for the changes can be previewed via
```
https://openfga.dev/pr-preview/pr-[number]
```

For example, previewing changes on PR-589 for changes on docs/modeling/public-access is available via
```
https://openfga.dev/pr-preview/pr-589/docs/modeling/public-access
```
