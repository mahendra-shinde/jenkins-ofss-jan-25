# DevOps with Jenkins

## Overview of DevOps

DevOps is a set of practices that combines software development (Dev) and IT operations (Ops). Its primary goal is to shorten the software development lifecycle and deliver high-quality software continuously. DevOps encourages collaboration between development and operations teams, automates workflows, and emphasizes iterative improvement.

### Key Principles of DevOps:

1. **Continuous Integration (CI):** Developers frequently integrate code changes into a shared repository, triggering automated builds and tests.
2. **Continuous Delivery (CD):** Ensures that code changes are automatically prepared for production release.
3. **Automation:** Automating repetitive tasks, such as builds, testing, and deployments, to enhance speed and reliability.
4. **Collaboration:** Promoting seamless communication and collaboration between teams.

## DevOps Workflows: CI & CD

### Continuous Integration (CI):

- Developers push their code changes to a version control system (e.g., GitHub, GitLab, or Bitbucket).
- Automated builds and tests run to validate code quality and functionality.
- CI ensures early detection of bugs, reducing integration problems.

### Continuous Delivery (CD):

- Extends CI by automating the deployment process.
- Code changes that pass the CI pipeline are deployed to staging or production environments.
- CD ensures that software is always in a deployable state.


## Introduction to Jenkins

Jenkins is an open-source automation server that enables developers to build, test, and deploy their software efficiently. It supports CI/CD workflows and integrates with a wide range of tools and plugins.

### Key Features of Jenkins:

- Extensible with a vast library of plugins.
- Easy installation and configuration.
- Supports distributed builds for scalability.
- Works with various version control systems and build tools.

## Jenkins Plugins

Plugins extend Jenkins’ functionality, allowing integration with various tools and services.

### Popular Jenkins Plugins:

1. **Git Plugin:** Enables integration with Git repositories.
2. **Maven Integration Plugin:** Facilitates building Maven projects.
3. **Pipeline Plugin:** Supports defining CI/CD pipelines as code.
4. **JUnit Plugin:** Collects and displays unit test results.
5. **Deploy to Container Plugin:** Automates deployment to application servers like Tomcat.

### Installing Plugins:

1. Navigate to **Manage Jenkins > Manage Plugins.**
2. Search for the desired plugin in the "Available" tab.
3. Select the plugin and click **Install without restart.**


## Jenkins Jobs

A Jenkins job represents a task or a process that Jenkins executes, such as building a project or running a script.

### Creating a Jenkins Job:

1. Go to the Jenkins dashboard and click **New Item.**
2. Enter a name for the job and select a job type (e.g., Freestyle project).
3. Configure the job:
   - Source Code Management: Specify the repository URL.
   - Build Triggers: Define triggers such as polling or webhook.
   - Build Steps: Add steps like invoking Maven goals or running scripts.
4. Save the job and click **Build Now** to execute it.

---

## Using Jenkins to Build a Maven Project

1. **Install the Maven Integration Plugin:**

   - Go to **Manage Jenkins > Manage Plugins.**
   - Install the "Maven Integration Plugin."

2. **Configure Maven in Jenkins:**

   - Navigate to **Manage Jenkins > Global Tool Configuration.**
   - Under "Maven," click **Add Maven.**
   - Provide a name and specify the Maven installation path or let Jenkins install it automatically.

3. **Create a Jenkins Job for Maven:**

   - Select **New Item > Freestyle project.**
   - Configure the job:
     - **Source Code Management:** Provide the Git repository URL.
     - **Build:** Add a build step to invoke Maven goals (e.g., `clean install`).
   - Save and build the job.

---

## Collect Unit Test Report

Jenkins can collect and display unit test reports to help identify failing tests.

1. **Configure JUnit Plugin:**

   - Install the "JUnit Plugin" from **Manage Plugins.**

2. **Collect Test Results:**

   - Add a "Post-build Action" in your job configuration.
   - Select "Publish JUnit test result report."
   - Provide the path to the test result files (e.g., `**/target/surefire-reports/*.xml`).

3. **View Test Results:**

   - After the build, navigate to the job's "Test Result" section to view detailed reports.

---

## Deploy to Tomcat Using Tomcat Manager Interface

Jenkins can automate deployments to a Tomcat server using the "Deploy to Container Plugin."

1. **Install the Deploy to Container Plugin:**

   - Go to **Manage Jenkins > Manage Plugins.**
   - Install the "Deploy to Container Plugin."

2. **Configure Tomcat Server:**

   - Ensure the Tomcat server is running and the `tomcat-users.xml` file is configured with manager credentials:
     ```xml
     <user username="admin" password="password" roles="manager-script"/>
     ```

3. **Set Up Deployment in Jenkins Job:**

   - Add a "Post-build Action" in your job configuration.
   - Select "Deploy war/ear to a container."
   - Provide the following details:
     - WAR/EAR files: Path to the build artifact (e.g., `**/target/*.war`).
     - Context path: Application context (e.g., `/myapp`).
     - Container: Tomcat version and credentials.

4. **Deploy Application:**

   - Save and build the job.
   - The application will be deployed to the Tomcat server automatically.
