# 😼 Yarn Package Manager
We use [Yarn Workspaces](https://classic.yarnpkg.com/en/docs/workspaces/) to separate code into packages within the same repository

Using the workspaces feature, Yarn does not add dependencies to `node_modules` directories in the package directories if not needed –  only at the root level, i.e., yarn hoists all dependencies to the root level `node_modules` folder

When developing with Docker containers, the container should have Yarn installed. To install Yarn locally, directions can be found [here](https://classic.yarnpkg.com/en/docs/install)

## Helpful Commands
### Information
#### **Mismatched Dependencies**
A good way to see if there are any mismatched dependencies
```bash
yarn workspaces info
```

### Workspace Specific Commands
#### **Run Command**
Runs a command on a specific workspace
```bash
yarn workspace [package-name] [command]
```
#### **Add or Remove Dependency**
Adds or removes a dependency to the specified package
> **Note:** Adding local packages should be done by specifying the locally-set version number. Otherwise yarn tries to find the dependency in the registry
```bash
yarn workspace [package-name] [add/remove] [dependency-name] [-D/--dev]
```

### Global Commands
#### **Add or Remove Dependency**
Adds or removes a dependency globally. This should be used with caution
```bash
yarn [add/remove] [dependency-name] -W [-D/--dev]
```
