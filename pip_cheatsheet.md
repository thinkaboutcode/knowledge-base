# Pip Cheat Sheet

## Basic Commands

| **Command**                    | **Description**                                        |
|--------------------------------|--------------------------------------------------------|
| `pip install [package-name]`   | Install a package.                                     |
| `pip uninstall [package-name]` | Uninstall a package.                                   |
| `pip freeze`                   | List installed packages with their versions.           |
| `pip show [package-name]`      | Show details about a package (version, dependencies).  |
| `pip list`                     | List all installed packages.                           |
| `pip check`                    | Verify installed packages have compatible dependencies.|

## Installing Specific Versions

| **Command**                                  | **Description**                                               |
|----------------------------------------------|---------------------------------------------------------------|
| `pip install [package-name]==[version]`      | Install a specific version of a package.                      |
| `pip install [package-name]>=[version]`      | Install a package version greater than or equal to a specific version. |
| `pip install [package-name]<=[version]`      | Install a package version less than or equal to a specific version.   |
| `pip install [package-name]~= [version]`     | Install a package with a version within a specific range.     |

## Upgrading and Downgrading Packages

| **Command**                    | **Description**                                      |
|--------------------------------|------------------------------------------------------|
| `pip install --upgrade [package-name]` | Upgrade a package to the latest version.       |
| `pip install [package-name]==[older-version]` | Downgrade a package to a specific version. |

## Requirements Files

| **Command**                    | **Description**                                                      |
|--------------------------------|----------------------------------------------------------------------|
| `pip freeze > requirements.txt`| Generate a `requirements.txt` file with installed packages and versions. |
| `pip install -r requirements.txt` | Install all packages listed in a `requirements.txt` file.       |
| `pip uninstall -r requirements.txt` | Uninstall all packages listed in a `requirements.txt` file. |

## Dependency Management

| **Command**                    | **Description**                                                      |
|--------------------------------|----------------------------------------------------------------------|
| `pip install [package-name] --no-deps` | Install a package without its dependencies.                  |
| `pip install [package-name] --force-reinstall` | Reinstall a package, even if it’s already installed.    |
| `pip install [package-name] --ignore-installed` | Install a package, ignoring the installed versions.      |
| `pip install [package-name] --upgrade-strategy eager` | Upgrade dependencies to the latest versions.          |

## Installing from Different Sources

| **Command**                                              | **Description**                                                      |
|----------------------------------------------------------|----------------------------------------------------------------------|
| `pip install [URL or path-to-tarball]`                   | Install a package from a URL or local archive file.                  |
| `pip install git+[repository-url]`                       | Install a package directly from a Git repository.                    |
| `pip install [package-name] --extra-index-url [url]`     | Install a package from an additional PyPI-compatible index.          |
| `pip install --no-index --find-links=[local-dir] [package-name]` | Install a package from a local directory, without using PyPI.  |

## Working with Virtual Environments

| **Command**                    | **Description**                                                      |
|--------------------------------|----------------------------------------------------------------------|
| `pip install [package-name]`   | Install a package in the current virtual environment.               |
| `pip list --local`             | List packages installed in the current virtual environment.         |
| `pip freeze > requirements.txt` | Generate `requirements.txt` from packages in the virtual environment. |

## Caching and Cleaning Up

| **Command**                    | **Description**                                                      |
|--------------------------------|----------------------------------------------------------------------|
| `pip cache list`               | List all items in the pip cache.                                      |
| `pip cache dir`                | Show the location of the pip cache.                                   |
| `pip cache remove [package-name]` | Remove a package from the pip cache.                            |
| `pip cache purge`              | Remove all items from the pip cache.                                  |

## Advanced Usage

| **Command**                    | **Description**                                                      |
|--------------------------------|----------------------------------------------------------------------|
| `pip search [query]`           | Search for packages on PyPI. (Deprecated)                            |
| `pip install --user [package-name]` | Install a package for the current user only.                  |
| `pip install [package-name] --pre` | Install pre-release versions of a package.                   |
| `pip install --trusted-host [hostname] [package-name]` | Install a package from a trusted host.                      |
| `pip install [package-name] --proxy=[proxy-url]` | Install a package using a proxy server.                    |

