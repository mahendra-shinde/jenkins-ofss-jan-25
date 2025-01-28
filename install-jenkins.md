# Local Jenkins Installation

## Jenkins Installation (Using WAR File)

Follow these steps to install Jenkins using the WAR file:

1. **Prerequisites:**

   - Ensure Java (JDK 11 or higher) is installed on your system.
   - Verify Java installation:
     ```bash
     java -version
     ```

1. **Download the Jenkins WAR file:**

   - Visit the official Jenkins website: [https://www.jenkins.io/download/](https://www.jenkins.io/download/).
   - Download the "Generic Java Package (.war)" file.

1. **Run the Jenkins WAR file:**

   ```bash
   java -jar jenkins.war
   ```

   - Jenkins will start on the default port (8080).

1. **Access Jenkins:**

   - Open a browser and navigate to: `http://localhost:8080`
   - Complete the setup wizard by entering the initial admin password (found in the console output or the `secrets/initialAdminPassword` file).

1.  **Install Plugins:**

    - Click `Install Suggested Plugins` and wait for installation to complete.

1. **Admin User:** 

    - You must create a new Admin User. Provide all details and click   "Continue"

1. **Tools configuration:**
    - On Jenkins Dashboard, click `Manage Jenkins` > `Tools`
    - Now, Configure three tools
      
      ```
      JDK Installations
        Name: Java17
        JAVA_HOME: C:\Program Files\Java\jdk-17
        
      Maven Installations:
        Name: M3
        MAVEN_HOME=D:\apache-maven-3.9.5
      ```
