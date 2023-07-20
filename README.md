# Sunil-Java_project
Dependencies for this Application are:

Java - 1.8jdk
•	sudo apt-get update
•	sudo apt-get install openjdk-8-jdk
•	java -version

Maven
•	sudo apt-get update
•	sudo apt-get install maven
•	mvn -version

MYSQL
•	sudo apt-get update
•	sudo apt-get install mysql-server
•	sudo mysql_secure_installation

Git
•	sudo apt-get update
•	sudo apt-get install git

Docker (Optional)
•	sudo apt update
•	sudo apt install apt-transport-https ca-certificates curl software-properties-common
•	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
•	sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
•	sudo apt update
•	sudo apt install docker-ce

Clone Repositroy
•	git clone https://github.com/suryaops22/Sunil-Java-_project.git

In the Dockerfile I have given Nexus Images so that we could Install Nexus Using Docker also. If you don't want to use Dockerfile you can use the traditonal way to download nexus in your Ubuntu Machine using the following steps:

Nexus Installation:

Nexus Intallation Using traditional way:
•	cd /opt
•	sudo wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz
•	sudo tar -xvzf latest-unix.tar.gz
•	cd /opt/nexus-3.x.y-z/bin (Replace the x.y.x with your version)
•	sudo ./nexus start
•	sudo ./nexus status

To allow the ufw:
•	sudo ufw allow 8081
•	sudo lsof -i :8081

Nexus Intallation Using Dockerfile:
•	docker build -t nexus .
•	docker run -d -p 8081:8081 --name nexuscontainer nexus
•	docker ps

Use the Browser to Create a Nexus Repository: http://localhost:8081
•	Username - admin
•	Password - Get into Docker container for Password:
o	docker exec -it nexuscontainer /bin/bash
o	cat /nexus-data/admin.password

Paste the password in Browser and create a new-password > Next > Enable anonymous access > Next > Finish.

To Create a Nexus Repository:
•	Settings > repositories > Create Repository > maven2(hosted) > Name: my-maven-releases > Create repository.

Settings.xml & pom.xml
Now edit the Nexus-Repo,Username,Password & add Ip address in the settings.xml file. 
Edit the content under repositories & Ip address in pom.xml file.

To build the package using maven:
•	mvn clean install

To Run the Application:
•	mvn jetty:run

To host the application paste the URL of Ip address in the browser : http://localhost:8080

To install maven in running jenkins container:
• docker exec -u 0 -it <jenkins-container-id> /bin/bash
• apt-get update
• apt-get install -y maven
• mvn --version

In order to commit this jenkins with maven container and create new image (containing jenkins and maven):
• docker commit <jenkins_container_id> <new_image_name>

Use any of the following docker run commands to create new container with the above new image:
• #docker run -d -p 1234:8080 -p 50000:50000 --name jenkinscontainer jenkins:maven
• docker run -d -p 1234:8080 --name jenkinscontainer jenkins:maven

