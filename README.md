# sample

DEVOPS

Program 6

JAVA
java -version (should be 17 or above)
sudo update-alternatives --config java

JENKINS
wget https://get.jenkins.io/war-stable/latest/jenkins.war
java -jar jenkins.war

( If jenkins is already there do the below )

dpkg -l | grep jenkins
sudo apt remove jenkins
rm ~/jenkins.war
rm -rf ~/.jenkins
java -version

LOCALHOST
http://localhost:8080

GIT 
git --version
sudo apt update && sudo apt install git -y

git config --global user.name "Harshini Asapu"
git config --global user.email "haas23ainds@cmrit.ac.in"
git config --global init.defaultBranch main

ssh-keygen -t rsa -b 4096 -C "haas23ainds@cmrit.ac.in" -f ~/.ssh/id_rsa -N ""

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub            (this generates a key) 


GITHUB

> Settings
> SSH and GPG keys
> Add the ssh key from the terminal there
> ssh key created

ssh -T git@github.com 

> Settings
> Developer settings
> Tokens classic
> Generate a New PAT Generate new classic token then enable all check boxes on GitHub
(Copy the new token generated and paste into any text file)

curl -H "Authorization: token ghp_TkRQBMqlun9M5hlakuuBztcT1SUS2xxxxxxx" \
-d '{"name":"hello-maven", "private":false}' \
https://api.github.com/user/repos


MAVEN

Step 1: create maven project
mvn archetype:generate -DgroupId=com.example -DartifactId=hello-maven -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
Step 2: cd hello-maven
Step 3: gedit pom.xml
Step 4: edit pom.xml, under <url> put

<properties>
<maven.compiler.source>1.8</maven.compiler.source>
<maven.compiler.target>1.8</maven.compiler.target>
</properties>

Step 5: mvn compile
Step 6: mvn test
Step 7: mvn package

git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/haas23ainds-dot/hello-maven.git
git push -u origin main

git add .
git commit -m "Added Maven project structure"
git push


CREATE A NEW JENKINS JOB

1. Log into Jenkins:
	Open your web browser and navigate to your Jenkins URL (http://localhost:8080)
	Log in with your admin credentials.

2. Create a New Job:
	On the Jenkins dashboard, click on “New Item”.
	Enter an Item Name: For example, Maven-CI 
	Select “Pipeline project”
	Select GitHub project
	Put Project url ( https://github.com/haas23ainds-dot/hello-maven.git)

3. Enter Pipeline script:

pipeline {
agent any
stages {
stage('Check') {
steps {
echo "Pipeline is running"
}
}
}
}
	Apply and save
	Build


Program 7

Ansible 
sudo apt update
sudo apt upgrade -y
sudo apt install ansible -y
ansible –version

hosts.ini content
> gedit hosts.ini 

[local]
localhost ansible_connection=local

Setup.yml content 
> gedit deploy.yaml

---
- name: Basic Server Setup
hosts: localhost
become: yes
tasks:
- name: Update apt cache
apt:
update_cache: yes
- name: Install curl
apt:
name: curl
state: present

run in terminal
ansible-playbook -i hosts.ini setup.yml

(if password is asked, type “root” without double quotes or enter your sudo password)


     

Program 9


Step 1: Open Azure DevOps
	Open browser 
	Go to https://azure.microsoft.com/en-us/products/devops/?nav=min
	https://portal.azure.com/?icid=devops#home

Step 2: Sign In / Create Microsoft Account
	Sign in using Microsoft account OR Create a new Microsoft account 

Step 3: Create Azure DevOps Organization
	Click Create Organization 
	Enter organization name 
	Select region 
	Click Create 

Step 4: Create a New Project
	Click New Project 
	Enter: Project name 
	Click Create 

Step 5: Explore Azure DevOps Services
	Explore the site


Program 10

1. Open Azure DevOps -> https://portal.azure.com/?icid=devops#home
2. Go to more services -> go to devops -> Azure DevOps organizations
-> view my organization 
3. New project -> Enter project name -> create
4. Go to pipelines -> create pipeline -> github yaml -> select repository -> approve and install -> don’t change code and click save and run
(for first time pipeline creation visit this site https://aka.ms/azpipelines-parallelism-request and fill the form)
Program 11

1. Go to organization setting -> settings -> off the “Disable creation of classic release pipelines” option
2. Go to pipeline -> release
3. Select new Release Pipeline


4. Select a successfully run pipeline as Artifact
5. Select “Add an Artifact “
6. Select a pipeline which is run successfully in “Source (build pipeline)”

7. Select “Add” -> Select “Add a stage “
8. Select Empty job on top right under “Select a template
9. Give a stage name “Stage 2 “ for example -> click save 

10. Select “Create release” option on top right
11. Select “Create”
12. In pipeline -> Releases, you will find Release -1

Program 12 (cont. of 11)


13. Go to deploy -> deploy multiple
14. Select Stage 
15. Select “Deploy “ and wait for sometime

16. In case of error (No image label found to route agent pool Hosted Windows 2019 with VS2019)
a)	edit release -> edit tasks 
b)	agent job ->  azure pipelines -> agent specification -> windows 2022 or ubuntu (change the OS to match your device) -> save
17. go back -> deploy -> deploy multiple -> Select Stage 
18. In pipeline -> Releases it shows a green tick and has run successfully


