# Automation your workflow with GitHub Actions

## Overview 

Github Actions is a powerful and flexible automation platform that allows developers to automate tasks directly from their repositories. This automation helps you to streamline development, reduce manual errors and increase the efficiency of your software development workflow. With GitHub Actions, you can easily create continuous integration and continuous deployment (CI/CD) pipelines to build, test, and deploy code on every pull request and deploy merged pull request to production. Beyond CI/CD, it can automate repository actions like posting comments, applying labels, or assign contributors and also add reviewers (to assess and approve changes) by listening to events such as pushes, pull requests, and issues

---

## Advantages of GitHub actions

* Managed Infrastructure - Github manages the infrastructure for you which includes setting up servers, scaling resources and managing environments for the workflows.
* YAML-based configuration - Your task is to write workflow configurations in yaml file.
* Automatic execution - Github Actions handles rest of the tasks:
  * Job execution within Virtual Machine.
  * Caching necessary dependencies.
  * Providing reports on outcomes such as logs, artifacts, and job status.
---

## Event Triggers
Workflows can be triggered by various events:
*   **Push Events:** Runs your workflow when you push a commit or tag, or when you create a repository from a template. Event filters can be used to run jobs only on specific branches (e.g., only the `main` branch) or ignore certain branches.
*   **Schedule Events:** Used for executing workflows on a specific schedule using cron jobs.
*   **Workflow Dispatch Events:** Used when you want to manually trigger and run a workflow.

---

## Core Concepts of GitHub Actions

*   **Workflows**          
It is an automated process capable of executing one or more jobs. Workflow is defined using YAML files located in the `.github/workflows` directory of your repository.

*   **Jobs**      
Jobs are defined within a workflow, a job consists of a series of individual steps executed on a specific environment. Jobs run in parallel by default.

*   **Steps**      
Steps are individual tasks executed sequentially within a job. For example, a step might clone the repository, Install dependencies or run tests.

*   **Runners**        
Runner is a virtual machine which is responsible for executing your workflows when triggered. GitHub automatically provisions runners based on runs-on configurations specified at job-level (For example:runs-on: ubuntu-latest) 

---

## Types of Runners

### 1. GitHub-Hosted Runners

* Are hosted and maintained by Github. GitHub provides set Virtual Machines with various configurations including different Operating Systems & software environments. 
* By deftlaut it provides new clean instance for each and every job execution.
* Linux and Windows runners are hosted on the Microsoft Azure platform, while macOS runners are hosted in GitHub's own macOS cloud.
* No need to manage infrastructure. But you cannot install system-level software or customize the runners beyond selecting the OS type.


























