# GitLab CI/CD

## Table of Contents
1. [Introduction to GitLab CI/CD](#1-introduction-to-gitlab-cicd)
2. [Installing GitLab CI/CD](#2-installing-gitlab-cicd)
3. [Understanding GitLab CI/CD Concepts](#3-understanding-gitlab-cicd-concepts)
    - [Variables and Object Usage](#variables-and-object-usage)
    - [Control and Loop Structures](#control-and-loop-structures)
4. [Setting Up a CI/CD Pipeline](#4-setting-up-a-cicd-pipeline)
5. [Integrating SAST and DAST](#5-integrating-sast-and-dast)
6. [Configuring a Self-Hosted Runner](#6-configuring-a-self-hosted-runner)
7. [Reuse Possibilities in GitLab CI/CD](#7-reuse-possibilities-in-gitlab-cicd)
8. [Limitations of GitLab CI/CD](#8-limitations-of-gitlab-cicd)
9. [Conclusion](#9-conclusion)

---

## 1. Introduction to GitLab CI/CD
GitLab CI/CD (Continuous Integration and Continuous Deployment) is a tool integrated into GitLab that helps automate the software development lifecycle. It allows developers to build, test, and deploy applications efficiently.

## 2. Installing GitLab CI/CD
To set up GitLab CI/CD, you need:
- A GitLab account
- A repository with a `.gitlab-ci.yml` file

### Installation Steps:
1. Install GitLab on a server (optional, if self-hosting):
   ```sh
   sudo apt update && sudo apt install gitlab-ce
   ```
2. Configure runners for CI/CD execution:
   ```sh
   sudo gitlab-runner register
   ```
3. Ensure GitLab has access to your repository and `.gitlab-ci.yml` file.

## 3. Understanding GitLab CI/CD Concepts

### Variables and Object Usage
GitLab CI/CD provides predefined and custom variables. These variables help store secrets, environment details, and other configurations.

#### Example:
```yaml
variables:
  MY_VAR: "Hello, GitLab!"
  OBJECT_VAR: "{\"key\": \"value\"}"
```

### Control and Loop Structures
GitLab CI/CD supports control structures like `only`, `except`, and loops with `parallel`.

#### Example:
```yaml
stages:
  - test
  - deploy

job:
  script:
    - echo "Running job"
  only:
    - main
```

## 4. Setting Up a CI/CD Pipeline
A basic GitLab CI/CD pipeline consists of a `.gitlab-ci.yml` file with multiple stages.

#### Example:
```yaml
stages:
  - build
  - test
  - deploy

build-job:
  stage: build
  script:
    - echo "Building project"

test-job:
  stage: test
  script:
    - echo "Running tests"

deploy-job:
  stage: deploy
  script:
    - echo "Deploying project"
```

## 5. Integrating SAST and DAST
Static Application Security Testing (SAST) and Dynamic Application Security Testing (DAST) help identify security vulnerabilities.

#### Enable SAST:
```yaml
sast:
  stage: test
  script:
    - gitlab-sast scan
```

#### Enable DAST:
```yaml
dast:
  stage: test
  script:
    - gitlab-dast scan --url https://example.com
```

## 6. Configuring a Self-Hosted Runner
To set up a self-hosted runner:
1. Install the runner:
   ```sh
   sudo gitlab-runner install
   ```
2. Register the runner:
   ```sh
   sudo gitlab-runner register --url https://gitlab.com/ --registration-token <TOKEN>
   ```

## 7. Reuse Possibilities in GitLab CI/CD
GitLab CI/CD offers various ways to reuse configurations, making pipelines more efficient and easier to maintain.

### Using YAML Anchors & Aliases
You can use YAML anchors (`&`) and aliases (`*`) to avoid repeating code.

#### Example:
```yaml
defaults: &defaults
  script:
    - echo "This is a reusable script"

job1:
  <<: *defaults
  stage: build

job2:
  <<: *defaults
  stage: test
```

### Using `extends`
The `extends` keyword allows you to inherit configurations from another job.

#### Example:
```yaml
.default-job:
  script:
    - echo "Default script"

test-job:
  extends: .default-job
  stage: test
```

### Including External YAML Files
GitLab CI/CD allows importing external YAML files to reuse pipeline configurations across projects.

#### Example:
```yaml
include:
  - project: 'namespace/project-name'
    file: '/path/to/.gitlab-ci-template.yml'
```

### Using `before_script` and `after_script`
You can define common pre- and post-scripts that run across multiple jobs.

#### Example:
```yaml
before_script:
  - echo "This runs before each job"

after_script:
  - echo "This runs after each job"
```

## 8. Limitations of GitLab CI/CD
- Limited free CI/CD minutes on GitLab SaaS.
- Some features require a paid plan.
- Complex YAML syntax for large pipelines.
- Self-hosted runners require extra maintenance.

## 9. Conclusion
GitLab CI/CD is a powerful tool for automating builds, tests, and deployments. By understanding its concepts and best practices, developers can enhance their DevOps workflows efficiently.

