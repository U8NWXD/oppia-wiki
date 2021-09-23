## Table of contents

* [Introduction](#introduction)
* [Unmanaged development dependencies](#unmanaged-development-dependencies)
* [Managed dependencies](#managed-dependencies)
  * [`start.py`](#startpy)
  * [`install_third_party_libs.py`](#install_third_party_libspy)
    * [Python packages](#python-packages)
    * [Node modules](#node-modules)
    * [Protobuf](#protobuf)
  * [`install_third_party.py`](#install_third_partypy)
    * [Manifest files](#manifest-files)
    * [Redis and Elasticsearch](#redis-and-elasticsearch)
  * [`install_backend_python_libs.py`](#install_backend_python_libspy)

## Introduction

At Oppia we have a lot of dependencies, and we have many different ways of managing them. Some of these dependencies are required for our production application, while others are only used for development. Below, we will discuss how all these dependencies are managed.

## Unmanaged development dependencies

Oppia has some development dependencies that the user has to manage themselves. These are:

* Python 3.7
* Google Chrome
* git
* Tools commonly found on Linux and MacOS systems like bash

In our [[setup instructions|Installing-Oppia]], we walk developers through installing these.

## Managed dependencies

The rest of Oppia's development and production dependencies are managed by the Oppia code. These dependencies are installed to the following places:

* `oppia_tools/` stores development tools that aren't used in production. This folder is a sibling of the repository root (`oppia/`), so if you are in the root of the repository, this folder is at `../oppia_tools/`. However, we'll use `oppia_tools/` here for simplicity.
* `third_party/python_libs` stores our production Python dependencies.
* `third_party/static` stores some of our production Node.js dependencies.
* `node_modules` stores more production Node.js dependencies. On developer machines, it also stores development dependencies.
* `third_party/` also stores some other production dependencies like protobuf files.

When you run `python -m scripts.start`, a chain of scripts installs and/or upgrades dependencies as necessary:

```text
          +----------+
          | start.py |
          +----------+
               |
               | calls install_third_party_libs.main() when start.py is executed or imported
               v
  +-----------------------------+
  | install_third_party_libs.py |
  +-----------------------------+
               |
               | main() calls install_third_party.main()
               v
    +------------------------+
    | install_third_party.py |
    +------------------------+
               |
               | main() calls install_backend_python_libs.main()
               v
+--------------------------------+
| install_backend_python_libs.py |
+--------------------------------+
```

We'll look at each of these scripts below.

### `start.py`

When you start a development server, you execute `scripts/start.py`. This file does not itself install any dependencies, but it contains a call to `install_third_party_libs.main()` that will be executed whenever `start.py` is executed, or even imported.

### `install_third_party_libs.py`

#### Python packages

Whenever `install_third_party_libs.py` is executed or imported, it installs some Python packages that are needed early by the installation process. Some are installed to `oppia_tools/`, and other are installed to `third_party/python_libs/`.

When `install_third_party_libs.main()` runs, it installs additional Python packages:

* Packages that need to be available on the system `PATH` are installed "globally" using pip (in practice these are installed into your virtual environment).
* Other packages are installed to `oppia_tools/`.

All of these Python packages are listed directly in the `install_third_party_libs.py` file.

For all the Python packages installed by this script, the version of the package is pinned (i.e. we always install the same version, even if a newer version is available). However, the dependencies of that package may not have pinned versions. For example, we depend on `pip-tools`, which in turn depends on `pip`. The `setup.py` in `pip-tools` does not specify a particular version of `pip` that it requires, so when we install `pip-tools`, we will install the latest version of `pip`. This can lead to test failures when a breaking change in `pip` is released.

#### Node modules

This script installs the frontend dependencies from `package.json` using `yarn`. The versions of all these Node.js modules are pinned by `yarn.lock`, and they get installed to `node_modules/`.

#### Protobuf

We also install the protoc and buf tools for protobuf (these versions are pinned). By the time we install those tools, we've already called `install_third_party.main()`, so we have downloaded the proto files. We use buf to generate code from those proto files (i.e. compile the proto files).

### `install_third_party.py`

#### Manifest files

We use a `manifest.json` file to specify other dependencies that we have but which aren't Python packages or Node.js modules. This file has a `dependencies` key, under which it has the following keys:

* `proto`: Files here are installed to `third_party/`
* `frontend`: Files here are installed to `third_party/static/`
* `oppiaTools`: Files here are installed to `oppia_tools/`

Under each of these keys is a collection of key-value pairs where each key is a dependency name and each value is an object describing how to download and install the dependency. We support three types of dependencies:

* Zip archives of files. The zip archive must expand to a single file or folder. The following keys are required in the object describing this dependency:

  * `version`: The dependency's version string.
  * `url`: The full URL to the zip archive.
  * `downloadFormat`: Must be set to `zip`.

  The object must specify one of the following keys:

  * `rootDir`: The base name of the expanded file or folder.
  * `rootDirPrefix`: The prefix of the base name of the expanded file or folder. The prefix concatenated with the version string should produce the full base name.

  The object must also specify one of the following keys:

  * `targetDir`: The base name to which the expanded file or folder should be renamed.
  * `targetDirPrefix`: The prefix of the base name to which the expanded file or folder should be renamed. The prefix concatenated with the version string should produce the full base name.

* Collections of files. The following keys are required in the object describing this dependency:

  * `version`: The dependency's version string.
  * `url`: The prefix of the URL to the files.
  * `downloadFormat`: Must be set to `files`.
  * `files`: List of the files to download. Each file will be downloaded from the URL formed by joining `url` with the item in `files`, using a slash (`/`) as a delimiter. Files are not renamed after they are downloaded.
  * `targetDirPrefix`: A string which, when suffixed with `version`, yields the base name of the folder to which each file will be downloaded.

* Tar archives of files. These work just like zip archives, except that there are no optional keys. Instead of the `rootDir`, `rootDirPrefix`, `targetDir`, and `targetDirPrefix` keys, these two keys are required:

  * `tarRootDirPrefix`: Same as `rootDirPrefix` for zip files.
  * `targetDirPrefix`: Same as `targetDirPrefix` for zip files.

New dependencies should not be added to `manifest.json`, as this method of installing dependencies is deprecated. Instead, you should use the [node modules](#node-modules) method.

#### Redis and Elasticsearch

We download and install the Redis CLI and Elasticsearch development server. We pin the versions of these dependencies that we install, but we don't automatically upgrade old versions. Specifically, we try to execute the Redis and Elasticsearch binaries. If the binaries execute successfully, then we don't install anything.

### `install_backend_python_libs.py`

This script installs the Python dependencies we need in production to `third_party/python_libs`. We define these dependencies using `requirements.in`, which lists the libraries we depend on directly. Then `install_backend_python_libs.py` runs `scripts.regenerate_requirements` to generate `requirements.txt`, which lists those direct dependencies, plus all the packages that our direct dependencies need, and so on. Both `requirements.in` and `requirements.txt` specify versions, so `requirements.txt` is analogous to `yarn.lock` in that it pins all the versions of all the Python packages we use in production.
