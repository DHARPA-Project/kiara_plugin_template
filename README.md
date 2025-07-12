# `kiara` plugin template

This repository contains the default template to create a `kiara` plugin from. By default, the template
configures the plugin project to be [MPL](https://www.mozilla.org/en-US/MPL/) licensed, if you don't want that, you will have to
replace the LICENSE file, as well as any mentions of the license throughout the project.

## Requirements

- `git`
- `uv`: https://docs.astral.sh/uv/

## Features

- pre-configured Github Actions:
  - code checks (tests, mypy, ruff)
  - Python & Conda package build (& release)
- example `kiara` module, pipeline & job description file
- automated test setup for example jobs

## How to get started?

First, pick a name for your plugin. Pick something short and clear, that describes what context the plugin contains modules 
or pipelines for, for example `language_processing`, or `astronomy`, or even something narrower-scoped and non-generic like `markus_thesis`...

### Create project skeleton

Once you have [uv](https://docs.astral.sh/uv/) installed, execute the following command in a terminal, in the folder you want to put the project directory:

```
$ uvx kiara plugin create [NAME_OF_PLUGIN]
```

If you have `kiara` already installed, you can also create a new plugin directly, without using `uv`:

```
$ kiara plugin create [NAME_OF_PLUGIN]
```

Answer all the questions this asks you:

```
You are about to create a new `kiara` plugin.

You'll be asked a series of questions; the answers will be used to prepare
a basic, pre-configured Python project.

For more information, visit:

https://github.com/DHARPA-Project/kiara_plugin_template

🎤 Your full name.
   Markus Binsteiner
🎤 Your email address.
   markus@frkl.dev
🎤 A short description of the plugin.
   A plugin containing modules for logic operations.
🎤 Your github username or organization.
   makkus
🎤 Your anaconda username or organization (optional).
   dharpa

...
...
...   
```

This should have created a folder `kiara_plugin.[NAME_OF_PLUGIN]`, containing the project skeleton as well as an initialized
git repository with a single commit. Enter that folder, and check that this is the case:

```
$ cd kiara_plugin.[NAME_OF_PLUGIN]
$ git log
──────────────────────────────────────────────────────────────────────────────────────────────────────────────
commit ae686c34e1f7a29ecb710c761fe158b0892b36a4 (HEAD -> develop, origin/develop)
Author: Markus Binsteiner <markus@frkl.io>
Date:   Thu Jul 10 23:28:46 2025 +0200

    chore: initial commit
```

At this point, you should be able to run `kiara` via `uv`, and its context should include your new plugin with a `dev` version:

```
uv run kiara --version

╭─ Version information ──────────────────────────────────────────────────────────────────────────────────────╮
│                                                                                                            │
│   kiara                           0.5.17                                                                   │
│                                                                                                            │
│   kiara_plugin.core_types         0.5.2                                                                    │
│   kiara_plugin.develop            0.5.3                                                                    │
│   kiara_plugin.[NAME_OF_PLUGIN]   0.1.dev0+d20250710                                                       │
│                                                                                                            │
│   python                          3.13.3 (main, Apr  9 2025, 04:03:52) [Clang 20.1.0 ]                     │
│                                                                                                            │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

### Further tasks

In addition to the project stub, this template also created a TODO.md file, which contains a list of
tasks to get the most out of this template:

- connecting / uploading to Github
- configuring package releases (PyPI & Anaconda)

Check out that file for more details, or read below for a less in-detail overview of what you should do next.

#### Create Github repository

Now go to the Github account you specified in your answer above and create a new repository with the name that is
displayed at the end of the previous command (your project name with a pre-fixed `kiara_plugin.`).

Add that repository as a remote to your local git repo, following the url Github displays, something like:

```
$ git remote add origin git@github.com:[GITHUB_USER]/kiara_plugin.[NAME_OF_PLUGIN].git
# or:
$ git remote add origin https://github.com/[GITHUB_USER]/kiara_plugin.[NAME_OF_PLUGIN].git
```

Then, push the initial version:

```
$ git push --set-upstream origin develop
```

Check the 'Actions' tab on your Github project and wait for the 3 workflow runs to successfully finish. 

This template comes with pre-configured Github Actions to:

- run tests on Linux, Windows & Mac OS X
- upload test coverage to [coveralls](https://coveralls.io)
- run mypy against your code to ensure the code is properly type hinted
- run the [`ruff`](https://docs.astral.sh/ruff/) linter to check for common code pitfalls
- run the [`ruff`](https://docs.astral.sh/ruff/) formatter
- build a pip & conda package for your plugin
- upload the pip & conda packages to [pypi](https://pypi.org) and (optionally) [conda-forge](https://conda-forge.org/) whenever a tag is created and pushed to the repo.

Now you can start working on your plugin. For further information, check out those links:

- kiara plugin development: https://docs.dharpa.org
- kiara plugin template features: (below, for now) 

#### Prepare PiPY release

First of all, if you don't have one, you need to create an account on [PyPI](https://pypi.org).

You need to create a [trusted publisher](https://docs.pypi.org/trusted-publishers/). Assuming this project does not exist
yet in your PyPI account, follow [this guide](https://docs.pypi.org/trusted-publishers/creating-a-project-through-oidc/) to set everything up.

Use those values in the form:

- `PyPI Project Name`: the name of your project (incl. the `kiara_plugin.` part), as specified under `project`/`name` in `pyproject.toml`
- `Owner`: the github user name you specified when creating the plugin from the template
- `Repository name`: same values as under `PyPI Project Name`
- `Workflow name`: `build-linux.yaml`
- `Environment name`: `pypi`


#### Prepare Anaconda release

TBD

## Usage documentation

### Release

Once configured (see above), a release of a new version of your plugin is simple, just create a new git tag and push to Github:

```
git tag 0.1.0 
git push --tags
```

This would kick of the Python (and, if configured, Conda) package release steps in the Github Actions configuration.

### Code linting & formatting

TBD

### Testing

TBD


