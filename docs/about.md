# About page

# karius-lis
Laboratory Information System (LIS) for sample receipt and accessioning to ensure robust sample handling at scale.

# Setup

## Prerequisites
1. Install [Docker for Mac](https://docs.docker.com/docker-for-mac/) (or equevalent if you're using Windows/Linux OS)

## Setup project
1. Clone the master branch: `git clone git@github.com:KariusDx/karius-lis.git`.
1. In the repository, run `bin/setup` to setup your local environment.
1. Run the [nginx-proxy](https://github.com/kariusdx/local-webdev)
1. Run `bin/run-local`

## Running on Windows
1. See `Bash on Ubuntu on Windows and Docker` section in Braavos repository

## Usage
1. Use `bin/run-node` with npm commands explained bellow - e.g. `bin/run-node npm run test:watch`.
* `npm run start` - Spins a webpack dev server at localhost:80. Hot module replacement and redux dev tools are enabled.
* `npm run build` - Compiles stylesheets and spins a webpack dev server at localhost:80. Hot module replacement or dev tools does not work.
* `npm run test` - Runs karma-mocha test suite once.
* `npm run test:watch` - Runs karma-mocha test suite every time you a save file.
* `npm run lint` - Lint all .ts[x] files.
* `npm outdated` - Gives a list of outdated NPM packages.

# Development

## Editor

Visual Studio Code is recomended IDE. Install `tslint` extension for Visual Studio Code.

## Swagger Code generator

To generate new TypesSript definitions from Swagger API definitions run following command:

```bash
bin/run-swagger-codegen
```

Unfortunatelly we're past the point where we can use code generator output directlly in our code.
Instead generator will create `Braavos-generatd.ts` file which we can use to curate `Braavos.ts`.

Things that we are not able to auto-generate from swagger today are:
* Generate enums for swagger type array of enums (rejectionReason for samples and packages)

## Installing NPM package
1. Install library `bin/run-node npm install --save[-dev] <packagename>`.
1. Run `bin/shrinkwrap` to update package.json and npm-shrinkwrap.json (forgetting to run npm shrinkwrap will cause TravisCI build to fail).
1. Install typescript definitions: `./bin/run-node npm install --save @types/<packagename>`.
1. Commit changes.

## Sentry error monitoring
Our deployments use Sentry for error monitoring for both front-end and backend errors. The error reporting client is called Raven.
[https://sentry.io/karius/](https://sentry.io/karius/)

# Deployment

See [Karius Online - Website Architecture](https://karius.atlassian.net/wiki/display/ENG/Karius+Online+-+Website+Architecture) on Confluence.

# E2E Tests

```
bin/run-e2e-tests
```

Debugging tests:
* Install RealVNC on host machine
* Run tests with `bin/run-e2e-tests`
* Run `docker port selenium 5900 to` get VNC server port
* Connect to VNC session running on `localhost:{port}` (default password is `secret`)
* You can examine browser output and console as needed

# Browser Debugging with VS Code

Assuming you have LIS already running locally:

1. Open Debug panel
1. Set breakpoint
1. Hit run button
1. Step through the code
1. Examine variables

![VS Code Debugger](docs/images/vs-code-debug.png "VS Code Debugger")
