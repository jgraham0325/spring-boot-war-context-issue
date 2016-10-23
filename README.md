# spring-boot-war-context-issue
Demonstrating an issue with the context not being set correctly for static resources when running as a war

Issue: When generating a war from a spring boot application and deploying it onto a standalone Tomcat, the static resources in folders are not accessible since the url doesn't contain the context.

e.g. http://localhost:8080/app/images/springboot.png

should be: http://localhost:8080/spring-boot-war-context-issue/app/images/springboot.png

Steps to reproduce:
1. Install local tomcat server (used apache-tomcat-7.0.72-windows-x64 in this example)
2. Clone this project and cd to the root folder (spring-boot-war-context-issue)
3. Run gradlew assemble
4. Take generated war file from spring-boot-war-context-issue/build/libs/spring-boot-war-context-issue.war and put it in tomcat webapps directory
5. Start Tomcat (apache-tomcat-7.0.72\bin\startup.bat)
6. Open browser and go to http://localhost:8080/spring-boot-war-context-issue/

Expected result:
Page opens and shows text with picture

Actual result:
Page opens but picture is not found because it's looking for http://localhost:8080/app/images/springboot.png instead of where it really is http://localhost:8080/spring-boot-war-context-issue/app/images/springboot.png

Notes:
- works fine using embedded Tomcat
- suspect it's something that must be configured in a XML file on standalone tomcat