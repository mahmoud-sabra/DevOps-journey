

# ***What is CI/CD?***

CI And CD is the practice of automating the integration of code changes from multiple developers into a single codebase. It is a software development practice where the developers commit their work frequently to the central code repository (Github or Gitlab). Then there are automated tools that build the newly committed code and do a code review, etc as required upon integration.

**The key goals of Continuous Integration are to find and address bugs quicker, make the process of integrating code across a team of developers easier, improve software quality, and reduce the time it takes to release new feature updates. Some popular CI tools are Jenkins, Gitlab-CI, .. etc**
### ***Continuous Integration***

There could be scenarios when developers in a team, work in isolation for an extended period and only merge their changes to the master branch once their work is completed. This not only makes the merging of code very difficult, prone to conflicts, and time-consuming but also results in bugs accumulating for a long time which are only identified in later stages of development. These factors make it harder to deliver updates to customers quickly.

With Continuous Integration, developers frequently commit to a shared common repository using a version control system such as Git. **A continuous integration pipeline can automatically run builds, store the artifacts, run unit tests, and even conduct code reviews using tools like Sonar. We can configure the CI pipeline to be triggered every time there is a commit/merge in the codebase.**

## ***Continuous Delivery***

Continuous delivery helps developers test their code in a production-similar environment, hence preventing any last-moment or post-production surprises. These tests may include UI testing, load testing, integration testing, etc. It helps developers discover and resolve bugs preemptively.

By automating the software release process, CD contributes to low-risk releases, lower costs, better software quality, improved productivity levels, and most importantly, it helps us deliver updates to customers faster and more frequently. If Continuous Delivery is implemented properly, we will always have a deployment-ready code that has passed through a standardized test process.

****CD**** or ****Continuous Delivery**** is carried out after Continuous Integration to make sure that we can release new changes to our customers quickly in an error-free way. This includes running integration and regression tests in the staging area (similar to the production environment) so that the final release is not broken in production. It ensures automation of the release process so that we have a release-ready product at all times and we can deploy our application at any point in time. 

Continuous Delivery automates the entire software release process. **The final decision to deploy to a live production environment can be triggered by the developer/project lead as required.** 
## ***Continuous Deployment

The final stage of CI and CD will be continuous deployment. It’s an extension of continuous delivery, which automate the proper code to the code repository, continuous deployment will automate the related app for production purpose because there is not having any manual gate at the stage of the pipeline before production, continuous deployment relies on high automation.

in simple language, it is a change of application that goes through the cloud which is carried by the developer and it will live within a few minutes of writing pass with the automated testing.

## ***CI and CD Workflow

The below image describes how Continuous Integration combined with Continuous Delivery helps quicken the software delivery process with lower risks and improved quality.
![[Pasted image 20241221155913.png]]

## ***What are the Benefits of CI/CD?***

Automated testing enables continuous delivery that ensures software quality and safety and increases code profitability in production. CI/ CD pipelines enable a much shorter time-to-market for new product features, resulting in happier customers and reducing the burden on development.  
The significant increase in overall delivery speed enabled by CI/CD pipelines improves a company’s competitive advantage.  
Automation allows team members to focus on what they do best, resulting in the best end products. Companies with a successful CI/CD pipeline can attract outstanding talent. By moving away from traditional waterfall methods, engineers and developers are no longer engaged in repetitive activities that are often highly dependent on completing other tasks


## ***What is Jenkins?

Jenkins is a self-contained, open source automation server which can be used to automate all sorts of tasks related to building, testing, and delivering or deploying software.

Jenkins can be installed through native system packages, Docker, or even run standalone by any machine with a Java Runtime Environment (JRE) installed.

### **Key Features of Jenkins**:

1. **Automates CI/CD Pipelines**
    
    - Jenkins is designed to automate repetitive tasks, including building code, running tests, and deploying applications.
2. **Plugin Ecosystem**
    
    - Jenkins has over 1,500 plugins, allowing integration with various tools like Git, Docker, Kubernetes, Maven, Gradle, and more.
3. **Cross-Platform**
    
    - It works on Windows, Linux, and macOS, making it highly versatile.
4. **Extensible**
    
    - It is highly customizable, letting teams adapt Jenkins to their specific needs.
### **Why Use Jenkins?**

- To automate the build and deployment process.
- To implement Continuous Integration and Continuous Delivery (CI/CD).
- To improve team productivity by detecting code issues early.
### **How Jenkins Works**

1. **Developer Pushes Code**
    
    - Code is committed to a version control system (e.g., Git).
2. **Trigger Build**
    
    - Jenkins detects the new code changes (via webhook or polling) and triggers a build.
3. **Build the Code**
    
    - Jenkins compiles the code using tools like **Maven** or **Gradle**.
4. **Test the Code**
    
    - Jenkins runs unit tests or integration tests using tools like **JUnit** or **Selenium**.
5. **Generate Artifacts**
    
    - The build artifacts (e.g., `.jar` or `.war` files) are stored in an artifact repository like Nexus or Artifactory.
6. **Deploy the Application**
    
    - Jenkins deploys the built code to a staging or production environment using tools like Docker or Kubernetes.

### **Benefits of Jenkins**

1. **Open Source and Free**
    - Highly accessible with no licensing cost.
2. **Easy to Install**
    
    - Comes with an easy-to-use web-based interface for setup and configuration.
3. **Integration-Friendly**
    
    - Connects seamlessly with Git, Docker, Kubernetes, and many other tools.
4. **Improved Code Quality**
    
    - Automates testing and code reviews, reducing bugs and issues.
### **Install**
```
[Linux](https://www.jenkins.io/doc/book/installing/linux/#setup-wizard)
```
[Debian Jenkins Packages](https://pkg.jenkins.io/debian/)

[jenkins/jenkins - Docker Image | Docker Hub](https://hub.docker.com/r/jenkins/jenkins)


-----

```
https://github.com/nigelpoulton/psweb.git
```

```
docker build -t testnode .
docker tag testnode ma7moudsabra/depiapp:v1
docker login -u $USERNAME -p $PASSWORD
docker push ma7moudsabra/depiapp:v1
```

```
 ALL=(ALL:ALL) NOPASSWD:ALL

```

## **Jenkinsfile**

# Comparison Between Scripted and Declarative Pipelines in Jenkins

## Overview
Jenkins pipelines provide a way to define and automate CI/CD workflows. There are two types of pipelines in Jenkins: **Scripted** and **Declarative**. Each has its strengths and use cases, which are compared below.
[Pipeline](https://www.jenkins.io/doc/book/pipeline/#pipeline-syntax-overview)
[Pipeline Syntax](https://www.jenkins.io/doc/book/pipeline/syntax/#_footnotedef_1)

---

## 1. **Scripted Pipeline**
- **Definition**: Scripted pipelines are written in Groovy and offer full control over the Jenkins pipeline process.
- **Syntax**: Flexible and based on pure Groovy scripting.
- **Complexity**: Requires programming knowledge; suitable for advanced users.
- **Structure**: Freeform; no predefined structure.
- **Error Handling**: Needs explicit implementation using `try/catch` blocks.
- **Flexibility**: Extremely flexible and powerful for complex workflows.
- **Example**:
  ```groovy
  node {
      stage('Build') {
          echo 'Building...'
      }

      stage('Test') {
          echo 'Testing...'
      }
      stage('Deploy') {
          echo 'Deploying...'
      }
  }

```

## 2. **Declarative Pipeline**

- **Definition**: Declarative pipelines provide a structured way to define pipelines with predefined syntax, focusing on simplicity and readability.
- **Syntax**: More strict, requiring pipelines to follow a specific structure.
- **Complexity**: Easier to learn and use; suitable for beginners and standard workflows.
- **Structure**: Requires `pipeline` block, with defined stages and steps.
- **Error Handling**: Built-in mechanisms like `post` for handling errors and post-build actions.
- **Flexibility**: Less flexible but encourages best practices and consistency.
```
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the code...'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh './gradlew build' // Example for a Java project using Gradle
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh './gradlew test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                sh './gradlew assemble'
            }
        }

        stage('Docker Build & Push') {
            environment {
                DOCKER_USER = 'ma7moudsabra'
                IMAGE_NAME = 'my-java-app'
            }
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t $DOCKER_USER/$IMAGE_NAME:latest .'
                echo 'Pushing Docker image to Docker Hub...'
                sh 'docker login -u $DOCKER_USER -p $DOCKER_PASSWORD'
                sh 'docker push $DOCKER_USER/$IMAGE_NAME:latest'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Example deployment command
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

```
Both Scripted and Declarative pipelines are powerful, but their use depends on the requirements:

- Choose **Scripted** for flexibility and control.
- Choose **Declarative** for simplicity and best practices.

what we need from agent 
- jdk
- ssh

```
docker run -d --rm --name=agent --publish 2200:22 -e "JENKINS_AGENT_SSH_PUBKEY=$(cat /var/lib/jenkins/.ssh/id_rsa.pub)" jenkins/ssh-agent

```