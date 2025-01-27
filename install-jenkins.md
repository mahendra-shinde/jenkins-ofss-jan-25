# Local Jenkins Installation

## Pre-requisites
1. Java 11 SDK (Java-8 no longer supported)
2. Apache Maven 3.x
3. Jenkins.WAR file downloaded from jenkins.io

## Steps

1. Download jenkins WAR file using URL `https://get.jenkins.io/war-stable/2.479.3/jenkins.war`

1. Open Command prompt and run following commands:

    ```
    javac --version
    cd Downloads
    java -jar jenkins.war
    ```
1. Copy the `initial password` (Left click to select,  rigt click to copy)
1. Press ESC
1.  Visit `http://localhost:8080` and use the password copied from command prompt.

1.  Click `Install Suggested Plugins` and wait for installation to complete.

1. You must create a new Admin User. Provide all details and click "Continue"

1. On Jenkins Dashboard, click `Manage Jenkins` > `Tools`

1. Now, Configure three tools
    ```
    JDK Installations
        Name: Java17
        JAVA_HOME: C:\Program Files\Java\jdk-17
        
    Maven Installations:
        Name: M3
        MAVEN_HOME=D:\apache-maven-3.9.5
    ```
