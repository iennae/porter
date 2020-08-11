---
title: QuickStart Guide
descriptions: Get started using Porter
---

So you're interested in learning more about Porter? Great! This guide will walk you through key concepts and use the porter CLI to illustrate those concepts. You will build a bundle from a template, install, upgrade, and uninstall the bundle. 

## Pre-requisites

Docker is currently a prerequisite for using Porter. Docker is used to package up the bundle. 

If you do not have Docker installed, go ahead and [get Docker](https://docs.docker.com/get-docker/). 

## Getting Porter

Next, you need Porter. Follow the Porter [installation instructions](/install/).

## Porter Key Concepts 

For this quickstart, the main concepts that you will learn about are bundles, actions, and mixins that you can take with bundles.

* Bundle 

A bundle is your application artifact, client tools, configuration and deployment logic packaged together in a bundle. 

* Actions

Actions are the different set of defined steps that you want to do with the bundle. The primary actions are install, upgrade, and uninstall. 

* Mixins

Mixins are the building blocks for authoring bundles. There are a number of mixins included by default and you can create new ones as well. Mixins help you define the bundle actions. 

## Introducing Porter the CLI

When you install Porter, you are getting the porter command line interface for building bundles. 

In general, the steps for creating a new bundle are:

* Create a new directory on your local file system. 
* Use the porter CLI with the create flag to initialize your project with a set of templates. 
* Customize the porter.yaml template. 
* Use the porter CLI with the build flag to generate the bundle. 

Let's walk through those steps in more detail. 

### Set up a project directory on your system. 

The syntax might be slightly different depending on your operating system. 

```
mkdir -p my-bundle/ && cd my-bundle/
```

### Use the porter CLI with the create flag initialize your project with a set of templates:

```
porter create
```

Create sets up a number of template files that you can customize. The manifest file, `porter.yaml` is a key component to the bundle. Generally, you will customize this to your specific needs. In this quickstart, we won't modify it. This file contains all the crucial metadata about our bundle including defining the bundle actions. You use mixins to help in the implementation of those actions. In the template that is generated, the `exec` mixin is used to run shell scripts and commands. 

One of the other files that is provided with the porter create is the `helpers.sh` file which is a shell script to define a set of "Hello World" type statements so that you can test out the porter steps without causing any changes to your system. 

### Use the porter CLI with the build flag to generate the bundle. 

```
porter build
```

## More Bundle Actions

So you built a bundle, but what can you do with it? Let's look at the primary bundle actions: install, upgrade and uninstall. We'll also use list and show to inspect the bundle. 

```
porter install
```


Run porter with the list flag:

```
porter list
```

Sample output:
```
NAME    CREATED         MODIFIED        LAST ACTION   LAST STATUS
HELLO   2 seconds ago   2 seconds ago   install       succeeded
```

Next, try running porter with the show flag:

```
porter show
```

Sample output:
```
Name: HELLO
Created: 22 seconds ago
Modified: 22 seconds ago
Last Action: install
Last Status: succeeded
``` 

```
porter upgrade
```

Sample output:

```
 porter upgrade
upgrading HELLO...
executing upgrade action from HELLO (bundle instance: HELLO)
World 2.0
World 2.0
execution completed successfully!
```

Re-run porter with the list and show flags. 

```
porter list
NAME    CREATED        MODIFIED         LAST ACTION   LAST STATUS
HELLO   1 minute ago   24 seconds ago   upgrade       succeeded

porter show
Name: HELLO
Created: 1 minute ago
Modified: 36 seconds ago
Last Action: upgrade
Last Status: succeeded
```

Finally, run porter with the uninstall flag:

```
porter uninstall
```

This will remove the bundle. Re-run porter with the list and show flags and see that it no longer shows the bundle installed. 

## Next Steps 

So in this quickstart, you learned how to use some of the features of the porter cli to build, inspect, install, upgrade and uninstall bundles. Next, you can learn more about customizing the porter manifest, building specific bundles and sharing bundles. 
