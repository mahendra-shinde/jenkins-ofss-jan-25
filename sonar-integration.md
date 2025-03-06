### Steps to Integrate Jenkins with SonarCloud for Java Project Scanning

#### Step 1: Install SonarQube Scanner for Jenkins Plugin
1. Navigate to **Manage Jenkins** → **Plugin Manager** → **Available Plugins**.
2. Search for **SonarQube Scanner for Jenkins** and install it.
3. Restart Jenkins if required.

#### Step 2: Configure SonarQube in Jenkins
1. Go to **Manage Jenkins** → **Configure System**.
2. Scroll down to **SonarQube Servers** and click **Add SonarQube**.
3. Provide the following details:
   - **Name**: `sonar1` (Logical name to identify this SonarQube instance)
   - **Server URL**: `https://sonarcloud.io`
4. Configure **Server Authentication Token**:
   - Click **Add** → **Jenkins** Credential Manager → **Secret Text**.
   - Use the **SONAR_TOKEN** generated in SonarCloud. This token was generated when new "manual project" was setup on SonarCloud.
   - Enter this token in Jenkins and assign it a descriptive ID (e.g., `sonar-token`).
   - Select this credential from the dropdown in Jenkins.
5. Click **Advanced** and set the following properties:
   - **Additional Parameter**: `-Dsonar.projectKey=org-mahendra_project2`
   - **Additional Analysis Property**: `sonar.organization=org-mahendra`
   > Kindly replace the projectKey and organization with your sonarcloud projectKey and organization. 

6. Click **Save** to apply changes.

#### Step 3: Update the Jenkinsfile in the Sample Java Project
Create or modify the `Jenkinsfile` in the **`Sample-library-api`** repository as follows:

```groovy
pipeline {
    agent any

    tools {
        // Specify the Maven version installed in Jenkins (e.g., M3)
        maven "M3"
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the GitHub repository
                git 'https://github.com/mahendra-shinde/sample-library-api/'
            }
        }
        stage('Build') {
            steps {
                // Execute Maven build
                bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('Code Analysis') {
            steps {
                // Run SonarQube analysis within the SonarQube environment
                withSonarQubeEnv('sonar1') {
                    bat "mvn sonar:sonar"
                }
            }
        }
    }

    post {
        // Archive test results and build artifacts after successful execution
        success {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}
```

#### Step 4: Create and Configure a New Jenkins Job
1. Go to **New Item** in Jenkins.
2. Choose **Pipeline** and provide a name (e.g., `Sample-library-api-pipeline`).
3. Select the **Pipeline Script from SCM** option:
   - SCM: **Git**
   - Repository URL: `https://github.com/mahendra-shinde/sample-library-api/`
   - Branch: Specify the desired branch (e.g., `main` or `sonar`).
4. Save and build the pipeline.

### **Notes and Best Practices**
- Ensure the `SONAR_TOKEN` has appropriate permissions for the organization and project in SonarCloud.
- Make sure Maven (`M3`) is correctly configured in Jenkins under **Global Tool 