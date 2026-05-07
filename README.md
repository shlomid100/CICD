# CICD, src's on /C/Users/Shlomo/vprofile-project
1. we will doo the CI/CD with Jenkins(like github actions) will do code build the code after change run unit tests package the code and deploy.
2. we create EC2 instance with jenkins on it with sshkey=cicdkey.pem, open 8080(jenkins) 22(SSH) to my IP - see below the user data we set on the ec2, open the Jenkins URL
3. Adding the tools to Jenkins Git/JDK/Maven
4. Create Job in Jenkins-- choose type Pipeline/Freestyle--source code(git) --trigger --build steps

















User Data for the jenkins EC2 create:
**************************************
#!/bin/bash --> must to recognized as script

apt update -y
apt install fontconfig openjdk-21-jdk wget -y

mkdir -p /etc/apt/keyrings

wget -O /etc/apt/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key --> download the repo key to the	specific location

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" > /etc/apt/sources.list.d/jenkins.list --> Adds the Jenkins repository to your 
 	                                                                                                                            system where Repos are defined in so apt can install Jenkins


apt update -y
apt install jenkins -y

systemctl enable jenkins
systemctl start jenkins
