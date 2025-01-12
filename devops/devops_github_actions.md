# Overview: Reusing Parts with GitHub Actions

GitHub Actions allows you to automate workflows for CI/CD, testing, deployment, and other tasks. To reuse parts of your workflow and make it modular, you can leverage **composite actions**, **reusable workflows**, and **environment variables**.

---

## Table of Contents
- [1. Composite Actions](#1-composite-actions)
- [2. Reusable Workflows](#2-reusable-workflows)
- [3. Workflow Templates](#3-workflow-templates)
- [4. Using Environment Variables and Contexts](#4-using-environment-variables-and-contexts)
- [5. Share Across Multiple Repositories](#5-share-across-multiple-repositories)
- [6. Benefits of Reusability](#6-benefits-of-reusability)
- [7. Key Differences](#7-key-differences)

---

## **1. Composite Actions**

A composite action is a custom, reusable GitHub Action defined in a repository. It allows you to group multiple steps together into a single reusable action.

### **Steps to Create a Composite Action**

1. Create a new repository or folder to store your composite action, typically in the `.github/actions/` directory.
2. Define the composite action in an `action.yml` file, specifying its name, inputs, and steps.
3. Use the composite action in workflows by referencing it through the repository and version.

```plaintext
#Folder structure
.github/
    actions/
        my-composite-action/
            action.yml
```

```yaml
#**Example (`action.yml`):**
name: Reusable Composite Action
description: Installs dependencies and runs tests
inputs:
  node-version:
    description: The Node.js version to use
    required: true
runs:
  using: "composite"
  steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: ${{ inputs.node-version }}

    - name: Install dependencies
      run: npm install

    - name: Run tests
      run: npm test
```

```yaml
name: CI Workflow

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Use Composite Action
        uses: ./.github/actions/my-composite-action # Reference the composite action, always looks for a action.yml file
        with:
          node-version: '16'
```

---

## **2. Reusable Workflows**

Reusable workflows allow you to share entire workflows across multiple repositories or within the same repository.

### **Steps to Create a Reusable Workflow**

1. Define the workflow in the `.github/workflows/` directory, using the `workflow_call` event to make it reusable.

```yaml
#Example (ci-build.yml):
name: CI Build
on:
  workflow_call:
    inputs:
      node-version:
        required: true
        type: string
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ inputs.node-version }}

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

2. Specify inputs for dynamic configuration, such as version numbers or environment settings.
3. Call the reusable workflow in other workflows by referencing it and passing the required inputs.

```yaml
jobs:
  use-reusable-workflow:
    uses: your-repo/.github/workflows/ci-build.yml@main
    with:
      node-version: 16
```

---

## **3. Workflow Templates**

A **workflow template** is a pre-defined workflow designed to be reused across multiple repositories. It allows you to provide a consistent base workflow structure, which can then be customized and adapted for individual repositories.

### **Key Features of Workflow Templates**
- **Predefined Workflow Setup**: A template provides a base set of steps and configurations, allowing you to quickly start a new workflow without needing to create everything from scratch.
- **Customization**: Templates are designed to be easily customizable to fit the specific needs of a new repository or project.
- **Repository or Organization-wide**: Workflow templates can be stored in a repository, or you can publish them within an organization for others to use.
- **Consistency**: Using templates ensures that all repositories in an organization or project adhere to the same best practices for workflow automation.

### **Use Case for Workflow Templates**
Imagine you have a common CI/CD pipeline that you want to apply across several repositories in your organization. Rather than manually creating the same workflow in each repository, you can create a **workflow template** that provides the base setup. Developers can then use the template to quickly add a CI/CD workflow to their repositories without re-creating the configuration each time.


## **4. Using Environment Variables and Contexts**

Environment variables help reuse parts of workflows dynamically by providing configurable values that can be accessed across steps.

### **Steps to Use Environment Variables**

1. Define environment variables at the workflow or job level.

```yaml
env:
  NODE_VERSION: 16
  APP_NAME: my-app

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}

      - name: Log Application Name
        run: echo "Building ${{ env.APP_NAME }}"
```

2. Reference these variables in steps to dynamically configure actions or log messages.
3. Combine environment variables with inputs for greater flexibility.

---

## **5. Share Across Multiple Repositories**

Reusable components, such as workflows or composite actions, can be shared across multiple repositories. This is done by storing them in a central repository and referencing them using the appropriate repository name and version tag.

---

## **6. Benefits of Reusability**

1. **Consistency**: Standardizes practices across multiple projects by reusing the same workflows or actions.
2. **Reduced Duplication**: Avoids repeating similar steps in every workflow, saving time and effort.
3. **Ease of Maintenance**: Updates to reusable components automatically apply wherever they are referenced.
4. **Modularity**: Breaks down complex workflows into smaller, reusable parts for better organization and clarity.

## **7. Key Differences**

| Feature                     | **Composite Actions**                          | **Reusable Workflows**                          | **Workflow Templates**                         |
|-----------------------------|-----------------------------------------------|------------------------------------------------|-----------------------------------------------|
| **Scope**                    | A group of steps that can be reused in workflows | A complete workflow with jobs and steps         | A pre-defined workflow that can be customized  |
| **Purpose**                  | To bundle tasks into reusable actions          | To reuse entire workflows across multiple repositories | To provide starting templates for workflows    |
| **Trigger**                  | Triggered as part of a job in a workflow       | Triggered by the `workflow_call` event          | Manually copied or referenced for reuse       |
| **Level of Reusability**     | Reusable within the same or different workflows | Reusable across repositories and workflows     | Reusable by others for creating new workflows  |
| **Customization**            | Supports inputs and outputs                   | Supports inputs and outputs                    | Customizable when copied into other repositories|
| **Common Use Cases**         | Small, modular actions (e.g., setup, tests)    | Full CI/CD pipelines, deployment workflows      | Standardizing workflows across repositories    |
| **Integration**              | Can be used with other actions within workflows | Can call multiple jobs and workflows            | Typically used to create new workflows         |
