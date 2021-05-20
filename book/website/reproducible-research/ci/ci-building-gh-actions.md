# Building a Block of a Github Actions

As described previously, workflow files use YAML syntax, which has either a `.yml` or `.yaml` file extension. If you're new to YAML and want to learn more, {ref}`see our section about YMAL<rr-renv-yaml>`. This workflow must be stored in the `.github/workflows` directory of your repository.

Each workflow is defined in a separate YAML. We will introduce the building block of a workflow using Hello World Example:

```
name:
    Hello World package
on:
  push:
    branches: [ master ]
Jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
```  

**1. name**

This is the name of the workflow and it is optional. GitHub will use this name to be displayed on the repository's actions page.
```
name:
    Hello World package
```

**2. on**

The `on` field tells GHA when to run. For example, we can run the workflow anytime there's a `push` or a `pull`.
```
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]
```
There are many events which can be used to trigger a workflow. You can explore them [here](https://docs.github.com/en/free-pro-team@latest/actions/reference/workflow-syntax-for-github-actions).

**3. jobs and steps**

This block defines the core component of an Actions workflow. Workflows are made of `jobs`. Every job also needs a specific host machine on which to run, the `runs-on:` field is how we specify it. The template workflow is running the `build` job in the latest version of Ubuntu, a Linux-based operating system.

```
jobs:
  build:
  runs-on: ubuntu-latest
```

We can also separate the `build` and `test` functions of our workflow into more than one job that will run when our workflow is triggered. Jobs are made of `steps`. These allow you define what to run in each job. There are three ways to define steps.

- With `uses`
- With `run`
- With `name`

```

jobs:
  build:
  runs-on: ubuntu-latest
  steps:
    - uses: actions/checkout@v2
  test:
    - name: npm install
      run: |
        npm install
        npm test
```

The is the most most basic action is `uses: actions/checkout@v2`. This use a community action called [`checkout`](https://github.com/actions/checkout) to allow the workflow to access the contents of the repository. You can also use `uses: ./action-a` which provides the relative path to the action we created in the `action-a` directory of the repository

Providing a comprehensive guide of all the available options is beyond the scope of this overview, and instead we would urge you to study the CI configuration of well established open source projects.