---
title: Examine porter.yaml
description: Examining the Porter YAML configuration
---

Let's look at one of the key components of a bundle - the manifest file that is created with `porter create` in `porter.yaml`.

```yaml

name: HELLO
version: 0.1.0
description: "An example Porter configuration"
tag: getporter/porter-hello:v0.1.0

mixins:
  - exec

install:
  - exec:
      description: "Install Hello World"
      command: ./helpers.sh
      arguments:
        - install

upgrade:
  - exec:
      description: "World 2.0"
      command: ./helpers.sh
      arguments:
        - upgrade

uninstall:
  - exec:
      description: "Uninstall Hello World"
      command: ./helpers.sh
      arguments:
        - uninstall
```

This example is directly after running `porter create` and should be modified and customized for your needs. These are not the only configuration options, but let's talk through this example.  

At the top, specific bundle metadata is defined:

```yaml

name: HELLO
version: 0.1.0
description: "An example Porter configuration"
tag: getporter/porter-hello:v0.1.0
```

The name configuration is the name of the bundle. This bundle is "HELLO" as in a hello world example. 

The version configuration follows [Semantic Versioning](https://semver.org). A specific version of a bundle provides a set of functionality. 

The description configuration provides addiitonal information about the bundle and its functionality. 

The tag configuration is used when the bundle is published to a registry in the format of `REGISTRY/IMAGE` or `REGISTRY/IMAGE:TAG`.

There are 3 actions defined: install, upgrade, and uninstall.  The functionality of each action is implemented separately through mixins. 

Mixins are the building blocks for authoring bundles. There are a number of mixins included by default and you can create new ones as well. In this example, the `exec` mixin is included:

```yaml

mixins:
  - exec
  ```

  and then invoked within the action, for example for install

  ```yaml

  install:
  - exec:
  ```

The `exec` mixin is used when you want to run shell scripts and commands. 

Each action may have one or more steps to accomplish that action. For the install action:

```yaml

install:
  - exec:
      description: "Install Hello World"
      command: ./helpers.sh
      arguments:
        - install
```

there is one step that uses the exec mixin to run the `helpers.sh` script with the argument `install`. Within your project directory, you will see the helpers.sh bash script.

Inside the `helpers.sh` file, install is a bash function:

```bash

install() {
  echo Hello World
}
```

This runs the echo built-in command with the arguments "Hello World". 