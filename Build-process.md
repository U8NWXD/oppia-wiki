## Table of contents

* [Introduction](#introduction)
* [Build script](#build-script)
* [Build modes](#build-modes)
  * [Build mode constants](#build-mode-constants)
  * [Dev mode](#dev-mode)
  * [Prod mode](#prod-mode)
    * [Plain prod mode](#plain-prod-mode)
    * [Minify only third-party libraries](#minify-only-third-party-libraries)
    * [Maintenance mode](#maintenance-mode)
    * [Deploy mode](#deploy-mode)
    * [Unused: Deparallelized terser mode](#unused-deparallelized-terser-mode)
* [Source maps](#source-maps)

## Introduction

Before we can run the Oppia server, we have to build it. This build process transforms the files defining our application (e.g. code, images, configuration files, etc.) from the developer-friendly format we store in GitHub into a form that can be executed to run the server. If you are running the local development server, this build process makes minimal changes, but when deploying to production, we do much more optimization.

This page documents how the build process works in each of its modes. For most developers the build steps are handled automatically and can be ignored; however, some bugs appear only in certain build modes. For example, a bug might only happen in prod mode, in which case a developer will be unable to reproduce it in dev mode.

## Build script

The build process is performed by [`scripts/build.py`](https://github.com/oppia/oppia/blob/develop/scripts/build.py). If you ever want to know exactly how a particular part of the build process works, you should check out the code there.

## Build modes

There are two primary build modes: dev mode and prod mode. When running in prod mode, you can also enable maintenance mode or deploy mode, or you can choose to only minify third-party libraries. This means the build mode hierarchy looks like this:

* Dev mode
* Prod mode
  * Maintenance mode
  * Deploy mode
  * Minify only third-party libraries

We use prod mode for most everything besides local development. For example, we use prod mode when deploying to production and testing servers, and we run most tests in prod mode. A notable exception is the lighthouse accessibility tests, which run in dev mode because they don't depend on prod mode, and dev mode compilation is faster.


### Build mode constants

The build mode affects the application during runtimes through the following constants in `assets/constants.ts`:

* `DEV_MODE`: Set to `true` if and only if we are in dev mode. Otherwise, this is `false`.
* `EMULATOR_MODE`: Set to `true` if and only if we are not in deploy mode. Note that being in deploy mode implies being in prod mode. Otherwise, this is `false`.
* `ENABLE_MAINTENANCE_MODE`: Set to `true` if and only if we are in maintenance mode. Note that being in maintenance mode implies being in prod mode. Otherwise, this is `false`.

### Dev mode

We use dev mode for local development. For example, when you run `python -m scripts.start`, you build the app in dev mode. This mode is optimized to build as quickly as possible, so it doesn't do much optimization. This means that the server doesn't run quite as quickly.

Here's what happens during a dev mode build:

1. Some third-party libraries are generated. If you recently ran the server, then there might not be much to change here. Otherwise, the third-party libraries from `manifest.json` are downloaded. Note that the libraries in `manifest.json` are just some of our frontend libraries. The downloaded CSS and JavaScript code files are combined into `third_party/generated/third_party.css` and `third_party/generated/third_party.js`, and the downloaded fonts are placed in `third_party/webfonts/`.
2. The build script sets the constants in `assets/constants.ts` to enable dev mode. Specifically, `DEV_MODE` is `true`, and the other constants are `false`.
3. [Webpack](https://webpack.js.org/) bundles our frontend code files and runs with a [configuration](https://github.com/oppia/oppia/blob/develop/webpack.dev.config.ts) designed for minimal compilation time. Note that the dev mode configuration file inherits from the [root webpack config file](https://github.com/oppia/oppia/blob/develop/webpack.common.config.ts). In dev mode, webpack runs in "watch" mode so that when files are changed, webpack re-builds the app automatically. Note that **this step is not handled by `build.py`.** Instead, this step is usually performed by whatever script you actually executed, for example `start.py`. When running the frontend tests, this step doesn't happen at all.
4. The `app_dev.yaml` configuration file for the app already exists, so it doesn't need to be generated.

### Prod mode

In prod mode, we more aggressively optimize the app for performance, but the cost of this optimization is that the build process takes longer. Prod mode is also a little more complicated because it has three additional options: minify only third-party libraries, maintenance mode, and deploy mode.

#### Plain prod mode

First, let's consider what happens in plain prod mode where those three options are all disabled:

1. The third-party libraries are generated like in [dev mode](#dev-mode), but they are also minified so they take up less space.
2. Hashes are generated for asset files like images. These will be used later.
3. [Webpack](https://webpack.js.org) runs with watch mode disabled and a configuration optimized for application performance.
4. `app.yaml` is generated from `app_dev.yaml`. The two files are identical in plain prod mode, except for a comment in `app.yaml` noting that it is auto-generated.
5. The third-party libraries, assets, files compiled by webpack, and some other files are all copied to a build folder `build/`. This mimics the build folder we generate and upload to production servers when deploying the app for real. During this process, asset files are renamed to include the hashes we generated earlier. This ensures that if the file content changes, the name changes, so any caches of the old file are invalidated.

This is the mode our tests run in (except the lighthouse accessibility tests), and it's what you'll want to use if you want to locally run a version of the app that's as close to the production version as possible. You can use this mode like this:

```console
python -m scripts.start --prod_env
```

#### Minify only third-party libraries

In this mode, the third-party libraries are installed and minified, but no other steps from [plain prod mode](#plain-prod-mode) happen. This is only used by the frontend tests.

#### Maintenance mode

As far as the build process is concerned, maintenance mode works just like [plain prod mode](#plain-prod-mode) except that the `ENABLE_MAINTENANCE_MODE` constant gets set to `true`. Then when the app runs, only admins can log in. We use this when we are upgrading the production server and need to let jobs run while ensuring users don't change any data.

This mode is used by our deployment scripts. You can also enable it locally like this:

```console
python -m scripts.start --prod_env --maintenance_mode
```

#### Deploy mode

Deploy mode is also very similar to [plain prod mode](#plain-prod-mode), except that the `EMULATOR_MODE` constant is set to `false`. Further, we make some changes to the `app.yaml` file:

* Remove the `version: default` line
* Remove the environment variables specified in the `ENV_VARS_TO_REMOVE_FROM_DEPLOYED_APP_YAML` constant in `build.py`. We remove these since they are already present in the production environment.

This mode is used by our deployment scripts.

#### Unused: Deparallelized terser mode

We used to use a `deparallelize_terser` mode when running the E2E tests on CircleCI, but since we don't run E2E tests on CircleCI anymore, this mode is unused and may be removed soon.

## Source maps

Even when running in dev mode, the code your browser runs does not look much like the code on your file system. Files have been combined, and in prod mode, they've been minified. To make debugging easier, you can generate source maps that map from the code your browser is running back to the code on your file system.

Generating source maps is expensive, so by default we don't make them. However, you can enable source map generation in both dev and prod modes, usually by passing a `--source_maps`, for example:

```console
python -m scripts.start --source_maps
python -m scripts.run_e2e_tests --prod_env --source_maps
```

With these flags, the `webpack.*.sourcemap.config.ts` configuration files are used to enable source mapping.
