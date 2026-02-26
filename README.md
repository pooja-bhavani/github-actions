# Automation your workflow with GitHub Actions

## Overview 

**GitHub Actions** is a powerful and flexible automation platform that allows developers to automate tasks directly from their repositories. This automation helps you to streamline development, reduce manual errors and increase the efficiency of your software development workflow. With GitHub Actions, you can easily create continuous integration and continuous deployment (CI/CD) pipelines to build, test, and deploy code on every pull request and deploy merged pull requests to production. Beyond CI/CD, it can automate repository actions like posting comments, applying labels, or assigning contributors and also add reviewers (to assess and approve changes) by listening to events such as pushes, pull requests, and issues.

---

## Advantages of GitHub actions

* Managed Infrastructure - Github manages the infrastructure for you which includes setting up servers, scaling resources and managing environments for the workflows.
* YAML-based configuration - Your task is to write workflow configurations in yaml file.
* Automatic execution - Github Actions handles rest of the tasks:
  * Job execution within Virtual Machine.
  * Caching necessary dependencies.
  * Providing reports on outcomes such as logs, artifacts, and job status.
---

## Core Concepts of GitHub Actions

###   **Workflows**          
It is an automated process capable of executing one or more jobs. Workflow is defined using YAML files located in the .github/workflows directory of your repository.

<img width="2778" height="583" alt="image" src="https://github.com/user-attachments/assets/833e7e71-2331-4491-ad9d-bac698ec1106" />

---

###   **Jobs**      
Jobs are defined within a workflow; a job consists of a series of individual steps executed in a specific environment. You can define multiple jobs which run in parallel by default.

<img width="1624" height="127" alt="image" src="https://github.com/user-attachments/assets/f2e1d295-7e57-4381-9d6c-f1f613b47872" />

The job fails because setps are not yet defined
<img width="831" height="126" alt="image" src="https://github.com/user-attachments/assets/8afd5410-4727-46ff-87f0-dcea2010105e" />

---

###   **Steps**      
Steps are individual tasks executed sequentially within a job. For example, a step might clone the repository, install dependencies or run tests.

<img width="1624" height="108" alt="image" src="https://github.com/user-attachments/assets/aaa052d0-2156-4f13-bf29-1cdb40d1861a" />


<img width="2933" height="1463" alt="image" src="https://github.com/user-attachments/assets/8bd1d606-9008-47aa-b8e5-7acc011726ad" />

---

###   **Runners**        
Runner is a virtual machine which is responsible for executing your workflows when triggered. GitHub automatically provisions runners based on runs-on configurations specified at the job level (For example:runs-on: ubuntu-latest)

<img width="2513" height="926" alt="image" src="https://github.com/user-attachments/assets/6369fcc4-0078-4aee-b4d9-d49d45253414" />


---

## Types of Runners

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/adb22caf-0969-4ed4-92a9-7efa5183048b" />

### 1. GitHub-Hosted Runners

* These runners are hosted and maintained by Github. GitHub provides set Virtual Machines with various configurations including different Operating Systems & software environments. 
* By default it provides new clean instance for each and every job execution.
* Linux and Windows runners are hosted on the Microsoft Azure platform, while macOS runners are hosted in GitHub's own macOS cloud.
* No need to manage infrastructure. But you cannot install system-level software or customize the runners beyond selecting the OS type.

### 2. Self-Hosted Runners

* These runners will run on your own infrastructure such as your own servers, VM’s, or cloud. You will have full control over the environment but you’re responsible for setting up and maintaining these runners.
* You can run multiple jobs on same machine
* You can install any required software and configure runner according to your requirements.

## Event Triggers
Workflows can be triggered by various events:
###   **Push Events** 
Runs your workflow when you push a commit or tag, or when you create a repository from a template. Event filters can be used to run jobs only on specific branches (e.g., only the `main` branch) or ignore certain branches.

<img width="1624" height="139" alt="image" src="https://github.com/user-attachments/assets/a46ffeba-1882-45b7-9815-e34b170c72ec" />


###   **Schedule Events** 
Used for executing workflows on a specific schedule using cron jobs.

<img width="2716" height="725" alt="image" src="https://github.com/user-attachments/assets/6acaa1bf-4366-429d-9c00-1342c3123f7f" />


 ###  **Workflow Dispatch Events** 
 Used when you want to manually trigger and run a workflow.

<img width="2915" height="1184" alt="image" src="https://github.com/user-attachments/assets/3d263e5f-a36c-4bc4-aba5-12fe3c332e64" />
<img width="2919" height="619" alt="image" src="https://github.com/user-attachments/assets/ab03103c-abc9-40e5-be6f-caa539932494" />

---

## Advanced Configuration
### Matrix Strategy

**Scenario**

You want to run the same job on multiple OS:
* Ubuntu 
* Windows
* macOS

If you want to build or test app on multiple OS you can define multiple jobs for each OS. But this would become more complicated because of repetitive lines or steps. 

**Solution:** To avoid repetitive lines or steps we make use of Matrix Strategy. This allows you to use variables in a single job definition which automatically creates multiple jobs that run in parallel. This is highly useful for testing an application across multiple operating systems simultaneously without writing repetitive code.

---

## Matrix Advanced Strategies
1. **Fail-Fast** - By default, if one job in a matrix fails, all in-progress jobs are automatically cancelled. Setting `fail-fast: false` disables this default behavior.

2. Max-parallel - Allows you to control the maximum number of jobs that will run simultaneously. Using matrix job strategy you can define the number here if you write 2 it will execute only 2 jobs. Once this is completed it will start executing the next set of jobs.


3. **Include and Exclude** - Use `exclude` to skip a specific combination. (Eg: If you don’t want to run the image in specific os use exclude) and `include` to add specific configurations (Eg: If you want to run new or same version of image in any os you use include).

<img width="2920" height="1285" alt="image" src="https://github.com/user-attachments/assets/920bc05a-8fe3-4481-a125-76c30b8ca30d" />

---
## Context

**What is context?**               
Context is a set of pre-defined objects and variables containing information about the workflow run. It can contain info about environments, events, variables, runtime env, secrets, jobs, steps etc. If you want to know the name of the runner, you can use runner.name and to know the operating system use runner.os. 

---

## Expressions

Expressions are used to dynamically configure workflows to execute jobs and steps based on conditional logic. For example, the `if` condition can determine whether a specific step or job should execute (e.g., only deploying if the branch is `main`).

Scenario: Deploy Only on Main Branch

You have:

Job 1 → Build Docker

Job 2 → Deploy

Deploy should run only on main. If any changes are made in a feature or any other branches, you don’t want to execute the deploy job.

---

## Secure AWS Deployment using OIDC

<img width="926" height="442" alt="image" src="https://github.com/user-attachments/assets/345addd6-7e98-44d6-87c7-7b1019cbaaff" />


OpenID Connect (OIDC) is a secure identity protocol that allows GitHub Actions to authenticate with AWS without needing to store long-term access keys (like the AWS secret key) in your repository.

**How it works:**

1. The GitHub Actions workflow requests an OIDC token from GitHub's OIDC provider.
2. The token (containing claims like the repository name and branch) is sent to AWS Secure Token Service (STS).
3. STS validates the token against the IAM role's trust policy.
4. Upon validation, STS issues temporary, limited-access AWS credentials.
5. The workflow uses these temporary credentials to access authorized AWS services (like S3 or ECR, etc.).
6. The credentials will automatically expire as soon as the job ends.







