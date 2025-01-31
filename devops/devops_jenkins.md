# Jenkins CI/CD Pipelines Tutorial

**Table of Contents:**
1. [Introduction to Jenkins CI/CD Pipelines](#1-introduction-to-jenkins-cicd-pipelines)
2. [Installing Jenkins](#2-installing-jenkins)
3. [Jenkins Pipeline Basics](#3-jenkins-pipeline-basics)
    - [Declarative vs. Scripted Pipelines](#declarative-vs-scripted-pipelines)
4. [Variables and Object Types in Jenkins Pipelines](#4-variables-and-object-types-in-jenkins-pipelines)
5. [Control and Loop Structures in Jenkins](#5-control-and-loop-structures-in-jenkins)
6. [Self-hosted Runners in Jenkins](#6-self-hosted-runners-in-jenkins)
7. [Limitations of Jenkins](#7-limitations-of-jenkins)
8. [Conclusion](#8-conclusion)

---

## 1. Introduction to Jenkins CI/CD Pipelines

Jenkins is an open-source automation server primarily used for continuous integration (CI) and continuous deployment (CD). It enables the automation of the software build, test, and deployment process. Jenkins CI/CD pipelines define a set of steps that are executed to achieve these goals.

### Key Concepts:
- **CI/CD**: Continuous Integration and Continuous Deployment.
- **Pipeline**: A series of automated steps that enable code to be built, tested, and deployed.
- **Jenkinsfile**: A file that defines a Jenkins pipeline.

---

## 2. Installing Jenkins

Before starting with Jenkins pipelines, you need to install Jenkins. Here's how to set it up:

### Steps:
1. **Install Java**: Jenkins requires Java to run. Make sure you have Java 8 or above installed on your machine.

   ```bash
   sudo apt install openjdk-11-jdk
   ```

2. **Install Jenkins**:
   For Debian-based systems (Ubuntu), use the following steps:

   ```bash
   wget -q -O - https://pkg.jenkins.io/keys/jenkins.io.key | sudo apt-key add -
   sudo sh -c 'echo deb http://pkg.jenkins.io/debian/ $(lsb_release -cs) main > /etc/apt/sources.list.d/jenkins.list'
   sudo apt update
   sudo apt install jenkins
   ```

3. **Start Jenkins**: Once installed, start Jenkins.

   ```bash
   sudo systemctl start jenkins
   sudo systemctl enable jenkins
   ```

4. **Access Jenkins**: Open a browser and go to `http://localhost:8080`. The first time you access Jenkins, it will ask for an unlock key, which you can get by running:

   ```bash
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   ```

5. **Install Plugins**: After logging in, Jenkins will prompt you to install recommended plugins. Click "Install" to proceed.

---

## 3. Jenkins Pipeline Basics

Jenkins pipelines are typically defined in a `Jenkinsfile`, which specifies the CI/CD steps. There are two types of pipelines: Declarative and Scripted.

### Declarative vs. Scripted Pipelines

#### Declarative Pipeline

The declarative pipeline is a simpler and more structured approach. It's easy to read and write, and it is the recommended style for most users.

```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building project...'
                // Build commands go here
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                // Test commands go here
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Deployment commands go here
            }
        }
    }
}
```

#### Scripted Pipeline

The scripted pipeline provides more flexibility and is a more programmatic approach, suitable for advanced use cases.

```groovy
node {
    stage('Build') {
        echo 'Building project...'
        // Build commands go here
    }
    stage('Test') {
        echo 'Running tests...'
        // Test commands go here
    }
    stage('Deploy') {
        echo 'Deploying application...'
        // Deployment commands go here
    }
}
```

---

## 4. Variables and Object Types in Jenkins Pipelines

### Variables in Jenkins Pipelines

Jenkins allows the use of variables within pipelines. Variables are often used to store values like build numbers, commit IDs, or environment-specific configurations.

```groovy
pipeline {
    agent any
    environment {
        MY_VAR = 'Some value'
    }
    stages {
        stage('Example') {
            steps {
                echo "My variable value is ${MY_VAR}"
            }
        }
    }
}
```

### Objects in Jenkins Pipelines

You can also use objects (maps, lists) in Jenkins pipelines. Here's an example using a map:

```groovy
def myMap = [name: 'John Doe', age: 30]

pipeline {
    agent any
    stages {
        stage('Print Object') {
            steps {
                echo "Name: ${myMap.name}, Age: ${myMap.age}"
            }
        }
    }
}
```

---

## 5. Control and Loop Structures in Jenkins

You can control the flow of your pipeline using conditions and loops.

### If-Else Condition

```groovy
pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'main') {
                        echo 'Main branch detected.'
                    } else {
                        echo 'Not the main branch.'
                    }
                }
            }
        }
    }
}
```

### Loops

You can use loops like `for` and `each` in Jenkins pipelines.

```groovy
pipeline {
    agent any
    stages {
        stage('Loop Example') {
            steps {
                script {
                    def list = ['step1', 'step2', 'step3']
                    for (item in list) {
                        echo "Running ${item}"
                    }
                }
            }
        }
    }
}
```

---

## 6. Self-hosted Runners in Jenkins

A **self-hosted runner** is a machine that you configure to run Jenkins jobs. This runner can be on any machine, whether it's a local machine, a cloud instance, or a server.

### Setting Up a Self-Hosted Runner

1. Go to `Manage Jenkins > Manage Nodes and Clouds > New Node`.
2. Choose the type of node (e.g., Permanent Agent).
3. Install the necessary agents or SSH into the runner machine and follow the installation instructions provided by Jenkins.

Once the runner is installed, you can assign it to specific pipeline stages using the `agent` directive.

```groovy
pipeline {
    agent {
        label 'my-self-hosted-agent'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Running build on self-hosted agent...'
            }
        }
    }
}
```

---

## 7. Limitations of Jenkins

While Jenkins is powerful, there are some limitations:

- **Complexity**: Jenkins can become complex to set up and maintain, especially in large-scale environments.
- **Scalability**: Managing many pipelines and agents can become difficult without proper scaling mechanisms.
- **User Interface**: Jenkins' UI can sometimes be unintuitive, especially for beginners.
- **Plugin Management**: Over-reliance on plugins can cause compatibility issues or performance degradation.

---

## 8. Conclusion

Jenkins is a versatile tool for implementing CI/CD pipelines. By mastering pipeline syntax, variables, loops, and setting up self-hosted runners, you can create automated workflows to build, test, and deploy your applications. Though Jenkins has its limitations, such as scalability and complexity, it remains a popular choice for many development teams due to its flexibility and powerful plugin ecosystem.

Start by setting up Jenkins, writing simple pipelines, and gradually experiment with more complex workflows as you gain experience. Happy automating!
