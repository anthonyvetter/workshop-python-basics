# Educates Workshop Template Repo

[Educates](https://docs.edukates.io/) is a lab platform that allows people to create technical lab workshops that utilize instructions and a linux terminal all in a self-contained web experience that runs on a Kubernetes cluster. 

This template repo is designed to enable people to do the following:

* get started quickly to create an Educates workshop
* run your workshop locally on your machine without needing to worry about Kubernetes cluster creation, setup, and Educates setup
* provide out of the box GitHub action workflows for best practice image building and tagging using GitHub Package registries



## Requirements

* [Docker Desktop](https://www.docker.com/get-started)
* [Kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl) version `1.21` or greater
* [Kind](https://kind.sigs.k8s.io/)

## Initial Setup

First things is to create your own GitHub repo for your project. Click the `Use this template` button
above in the GitHub UI and follow the steps create a repo in the organization you wish and with a unique
name is approprate for the workshop you're creating (do not leave it named `edu-educates-tamplate`).

After that is completed you can then clone that repo to your machine and make some initial file changes:

* `/Makefile.env` - Change these values to match the organization and name of the repo you created from the template
* `/workshop-resources/training-portal.yaml` - follow the `TODO` comments to update the Educates config file approppiately
* `/workshop-resources/workshop-deploy.yaml` - follow the `TODO` comments to update the Educates config file approppiately

After the above changes are made and saved we can now start up the environment to make sure the workshop starts correctly
before maaking any content/instruction changes. To start the workshop simply run `make` root directory of your repo.

```
make
```

Once complete towards the end of the command output a URL will be printed that you can browse to access the workshop.
You can confirm everything came up and then you'll want to commit those changes by themself so then you can start
on content related changes.

## Authoring Workshop Instructions

All the instructions for your workshop can be found in the `/worksop-instructions` directory. It's made up of two parts
and the Educates documentation for each is linked below:

* [content](https://github.com/eduk8s/lab-markdown-sample/blob/master/workshop/content/exercises/01-sample-content.md)
* [structure of content](https://docs.edukates.io/en/latest/workshop-content/workshop-config.html#specifying-structure-of-the-content)

After making content related changes if you want to see the results refreshed in a running workshop perform the following
two things:

* run `make refresh` from the terminal in the root of your repo
* run `update-workshop` from the terminal of the running workshop

## Changing the Workshop Definition

The characteristics of the worshop are controlled by the
[Workshop Definition](https://docs.edukates.io/en/latest/runtime-environment/workshop-definition.html)
which is found at `/workshop-resources/workshop-deploy.yaml`. We alread made basic name changes to it.
If you require addition features or configuration refer to the linked documentation and update according.

If you want to see those changes reflected, the workshop will need to be rebuilt and restarted, this can be done
by doing the following:

* run `make reload` from the terminal in the root of your repo
* terminate your runing workshop and launch a new one

## Cleaning up, Reclaiming Resources, and recovering when things go wrong

When you are done working on a workshop and want to shut everything down and reclaim resources that it
takes to keep the Educates platform running or just get into a state where something is not working run
the following command:

```
make kind-delete
```

To start things back up in the future you can always run `make` and the startup time will be quicker
than before because lots of images will have been cached on your machine as opposed to the first time.

## Commands
### Build and Run Locally
```
make
```
## Rebuild, and redeploy the workshop and training portal with changes
```
make reload
```
## Refresh the content in existing deployment
```
make refresh
```
After running the refresh, run `update-workshop` in your workshop terminal
window and refresh the browser. The educates documentation has more details on
[live updates to content](https://docs.edukates.io/en/latest/workshop-content/working-on-content.html#live-updates-to-the-content)
 as well.
### Stop an existing educates cluster
```
make stop
```
## Start a previously stopped educates cluster
```
make start
```
## Delete local educates cluster
```
make delete
```
## Delete local educates cluster and local registry
```
make clean
```
## Resources

* [Educates](https://docs.edukates.io/)