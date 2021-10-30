# Discovering the differences between Workspaces and Caching on CircleCI

## Introduction

This article looks at the differences between workspaces and caching on CircleCI.

The CircleCI definitions are:

> A [workspace](https://circleci.com/docs/2.0/glossary/#workspace) stores data unique to the job which may be needed in downstream jobs.

> [Caching](https://circleci.com/docs/2.0/caching/) is 
one of the most effective ways to make jobs faster by reusing the data from expensive fetch operations from previous jobs.

To understand workspaces and caching, the user also needs to understand [workflows](https://circleci.com/docs/2.0/workflows/) and [artifacts](https://circleci.com/docs/2.0/artifacts/). 

## What is a workspace?

Workspaces pass data. The data is unique for a run and is required for downstream jobs. 

Workspaces persist data between jobs in a single workflow. 

### Creating a workspace

1. Declare a workspace in a job
2. Add files and directories to the workspace.
3. Downstream jobs use this workspace for their own needs or add more layers on top.

A workspace is an additive-only store of data.

Downstream jobs can attach the workspace to their container filesystem. Attaching the workspace downloads and unpacks each layer based on the ordering of the upstream jobs in the [workflow graph](https://circleci.com/docs/2.0/workflows/#using-workspaces-to-share-data-among-jobs).


## What is caching?

Caching enables the user to store data through a hierarchy of files, using a key. The first time a job is run, the required data is downloaded and cached, storing the data for reuse. As the cache already exists subsequent job runs will be faster as the required data does not need to be downloaded again.

Caching persists data between the same job in different workflow builds.

## Summary

Workspaces persist data between jobs in a single workflow whereas caching persists data between the same job in different workflow builds.


## Further reading

+ [FAQ: Caching, workspaces and artifacts](https://circleci.com/docs/2.0/runner-faqs/#how-do-caching-and-workspaces-and-artifacts-work-with-circleci-runner)
+ [Workspaces and Optimization](https://circleci.com/docs/2.0/optimizations/#workspaces)
+ [Using workspaces to share data among jobs](https://circleci.com/docs/2.0/workflows/#using-workspaces-to-share-data-among-jobs)
+ [When to use caching, artifacts and workspaces](https://circleci.com/blog/persisting-data-in-workflows-when-to-use-caching-artifacts-and-workspaces/)
+ [Workflows](https://circleci.com/docs/2.0/workflows/) 
+ [Artifacts](https://circleci.com/docs/2.0/artifacts/)