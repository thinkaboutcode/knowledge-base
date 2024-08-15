# NPM Cheat Sheet

## Basic Commands

| **Command**                     | **Description**                                           |
|---------------------------------|-----------------------------------------------------------|
| `npm init`                      | Initialize a new Node.js project and create a `package.json` file. |
| `npm install [package-name]`    | Install a package locally in the current project.         |
| `npm uninstall [package-name]`  | Uninstall a package from the current project.             |
| `npm update [package-name]`     | Update a package to its latest version.                   |
| `npm install`                   | Install all dependencies listed in the `package.json` file. |
| `npm list`                      | List installed packages in the current project.           |

## Installing Specific Versions

| **Command**                     | **Description**                                           |
|---------------------------------|-----------------------------------------------------------|
| `npm install [package-name]@[version]` | Install a specific version of a package.        |
| `npm install [package-name]@[tag]`     | Install a package based on a tag (e.g., `beta`, `latest`). |

## Global vs Local Installation

| **Command**                     | **Description**                                           |
|---------------------------------|-----------------------------------------------------------|
| `npm install -g [package-name]` | Install a package globally, making it available system-wide. |
| `npm install [package-name]`    | Install a package locally, specific to the project.       |
| `npm list -g --depth=0`         | List globally installed packages.                         |
| `npm uninstall -g [package-name]` | Uninstall a globally installed package.                 |

## Managing Dependencies

| **Command**                     | **Description**                                           |
|---------------------------------|-----------------------------------------------------------|
| `npm install [package-name] --save` | Add a package as a dependency in `package.json`.   |
| `npm install [package-name] --save-dev` | Add a package as a development dependency in `package.json`. |
| `npm uninstall [package-name] --save` | Remove a package and update the `package.json`.   |
| `npm prune`                     | Remove extraneous packages not listed in `package.json`.  |

## Package Versioning

| **Command**                     | **Description**                                           |
|---------------------------------|-----------------------------------------------------------|
| `npm outdated`                  | Check for outdated packages in your project.              |
| `npm update [package-name]`     | Update a specific package to the latest version.          |
| `npm install [package-name]@[version-range]` | Install a package within a specific version range (e.g., `^`, `~`). |

## Scripts

| **Command**                     | **Description**                                           |
|---------------------------------|-----------------------------------------------------------|
| `npm run [script]`              | Run a script defined in `package.json` under `scripts`.   |
| `npm test`                      | Run the test script defined in `package.json`.            |
| `npm start`                     | Run the start script defined in `package.json`.           |
| `npm stop`                      | Run the stop script defined in `package.json`.            |

## Working with the NPM Registry

| **Command**                     | **Description**                                           |
|---------------------------------|-----------------------------------------------------------|
| `npm publish`                   | Publish your package to the npm registry.                 |
| `npm unpublish [package-name]`  | Remove a published package from the npm registry.         |
| `npm login`                     | Log in to your npm account.                               |
| `npm logout`                    | Log out of your npm account.                              |
| `npm whoami`                    | Show the logged-in npm user.                              |

## Cache Management

| **Command**                     | **Description**                                           |
|---------------------------------|-----------------------------------------------------------|
| `npm cache clean --force`       | Clear the npm cache.                                      |
| `npm cache verify`              | Verify the contents of the npm cache.                     |

## Versioning & Tagging

| **Command**                     | **Description**                                           |
|---------------------------------|-----------------------------------------------------------|
| `npm version [new-version]`     | Bump the version in `package.json`, create a git tag, and commit. |
| `npm dist-tag add [package-name]@[version] [tag]` | Add a distribution tag to a package version. |
| `npm dist-tag rm [package-name] [tag]` | Remove a distribution tag from a package version. |

## Auditing & Security

| **Command**                     | **Description**                                           |
|---------------------------------|-----------------------------------------------------------|
| `npm audit`                     | Run a security audit of your project's dependencies.      |
| `npm audit fix`                 | Automatically fix security vulnerabilities.               |

## Miscellaneous Commands

| **Command**                     | **Description**                                           |
|---------------------------------|-----------------------------------------------------------|
| `npm help`                      | Get help with npm commands.                               |
| `npm config set [key]=[value]`  | Set a configuration value for npm.                        |
| `npm config get [key]`          | Get the value of a configuration key.                     |
| `npm info [package-name]`       | View information about a package in the npm registry.     |
| `npm bin`                       | Display the location of the locally installed npm executables. |

