# 🐳 Docker Container Development
The following commands will allow you to use Docker for local development. All `make` commands must be run within `apps/marketplace-web`
## Getting Started
### Installation
To run the `make` commands, Docker will need to be installed locally. Installation packages and instructions can be found [here](https://docs.docker.com/get-docker/)
### Make Commands
#### **Install Dependencies**
Executes commands to install dependencies
```bash
make install
```
#### **Build Application**
Executes commands to serve application on port `3000`. Server should restart automatically if the server file is updated
```bash
make docker-run
```


## Development Flow
### Make Commands
#### **Bundle Application**
Executes commands to bundles client and server using Webpack build and watches for file changes
```bash
make docker-run-dev
```
#### **Serve Storybook**
Executes commands to start Storybook server within the Docker container on port 6006. **This requires the container to be running first using `make docker-run`**
```bash
make docker-run-storybook
```
#### **Enter into Container**
Executes commands to open a `bash` terminal inside the container. This will allow you to execute commands inside the container
```bash
make ssh
```