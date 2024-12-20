#

#   Tomcat installation on EC2 instance

## Prerequisite

### Install Java on an Ubuntu ec2 server. 

        sudo apt update

Add required dependencies for the jenkins package

    sudo apt install fontconfig openjdk-17-jre -y

Verify Java Installation 

    java -version 



## Downlowd and Install Tomcat App on the EC2

Download Tomcat v9.0.98 

    wget https://downloads.apache.org/tomcat/tomcat-9/v9.0.98/bin/apache-tomcat-9.0.98.tar.gz

Unzip the downloaded **.tar.gz ** zip file 

    tar -xvzf apache-tomcat-9.0.98.tar.gz

Move the extracted  binaries to desired Tomcat location

    sudo mv apache-tomcat-9.0.98 /opt/tomcat

Make the  Start / Stop scripts executable:

    chmod +x /opt/tomcat/bin/*.sh


Create link files for tomcat startup.sh and shutdown.sh

    ln -s /opt/tomcat/bin/startup.sh /usr/local/bin/tomcatup

    ln -s /opt/tomcat/bin/shutdown.sh /usr/local/bin/tomcatdown

    tomcatup


Access Tomcat Application from brower on default port 8080  **http://`<server-ip>`:8080**


**Note** (
Tomcat by default does not allow browser based login. Changing a default parameter in context.xml will resolve this issue. 
Find the **context.xml** file, and comment () Value ClassName field on files which are under webapp directory e.g. **manager/META-INF/context.xm**. 
After that restart tomcat services to effect these changes

    find / -name context.xml



In the tomcat home directory **/opt/tomcat/conf** , update users information in the **tomcat-users.xml**

    <role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<role rolename="manager-jmx"/>
	<role rolename="manager-status"/>
	<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
	<user username="deployer" password="deployer" roles="manager-script"/>
	<user username="tomcat" password="s3cret" roles="manager-gui"/>
