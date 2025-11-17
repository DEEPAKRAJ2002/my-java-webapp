**Prerequisites**
1. Jenkins
2. Maven
3. Tomcat

**Roles needs to be added for tomcat user you are using to deploy this application**
1. manager-gui - allows access to the HTML GUI and the status pages
2. manager-script - allows access to the text interface and the status pages
3. manager-jmx - allows access to the JMX proxy and the status pages
4. manager-status - allows access to the status pages only

**To run this project manually**
1. git clone https://github.com/DEEPAKRAJ2002/my-java-webapp.git
2. cd my-java-webapp
3. mvn clean package
4. cp target/my-webapp.war /var/lib/tomcat10/webapps/
5. sudo systemctl restart tomcat

-> See website in tomcaturl/my-java-webapp

**To run this project using pipeline**
**Plugin needed for jenkins**   
   1. Git
   2. Maven
   3. Deploy to container
1. Create pipeline project with Jenkinsfile given in this repository and build the job
