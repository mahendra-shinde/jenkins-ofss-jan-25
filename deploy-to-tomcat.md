# Deploying Java Web Application on Tomcat

## Plugins Required

- Deploy to Container

1. Create a new FreeStyle Project

  ```yaml
  Source-Code-Management:
    git: https://github.com/shinde-mahendra/ci-servlet-demo.git
  Build-Environment: Delete workspace before build
  Build Steps:
    Top-Level-Maven-Target:
      Maven: M2
      Goal: package
     Windows Batch Command:
       Command: copy target\ROOT.war mahendra.war  # Replace mahendra with your name
   Post-Build-Steps:
        deploy-war/ear-to-container:
           war-file: mahendra.war  # Replace mahendra with your name
           container:
              Add-Container: choose Tomcat 9.x
              Credential : Add new username & password 'manager'
              Tomcat-URL: http://20.219.205.194:8080/manager/text
  ```
1. Click `Create` or `Save` button and then try `Build Now`

1. To verify if your application is deployed on tomcat, Visit tomcat manager `http://20.219.205.194:8080/manager/html` and use credentials `manager/manager`
    Then click `List Applications`