# 💻 Local Node Development
Although it is suggested to use Docker locally ([guide](../docker/README.md)), it is possible to setup and run our application locally outside of a Docker Container

## Getting Started
Yarn must be installed locally to setup and run our application Directions can be found [here](https://classic.yarnpkg.com/en/docs/install)
### Installation
Install and build all packages and apps
```bash
yarn setup
```

## Development Flow
### Compile Applications Once
Compile both client and server applications for the marketplace. This command must be run inside `apps/marketplace-web`
```bash
yarn build
```
### Compile Application and Watch
Compile both client and server applications for the marketplace. The build process should execute again after any changes locally. This command must be run inside `apps/marketplace-web`
```bash
yarn build:watch
```
### Start Application
Start local web application. The server should restart if there are any changes to the build output. This command must be run inside `apps/marketplace-web`
```bash
yarn start
```
### Run Tests
Run tests on entire application or specific test suite. This command must be run inside `apps/marketplace-web`
```bash
yarn test [file-path]
```
### Audit Application
Compile application and output statistics on dependencies
```bash
yarn build:audit
```