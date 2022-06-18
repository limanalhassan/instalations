## Apache Maven Installation And Setup In AWS EC2 Redhat Instnace.
##### Prerequisite
+ AWS Acccount.
+ Create Redhat EC2 T2.medium Instnace with 4GB of RAM.
+ Create Security Group and open Required ports.
   + 22 ..etc
+ Attach Security Group to EC2 Instance.
+ Install java openJDK 1.8+

### Install Java JDK 1.8+  and other softares (GIT, wget and tree)

``` sh
# install Java JDK 1.8+ as a pre-requisit for maven to run.

sudo hostname maven
cd /opt
sudo yum install wget nano tree unzip git-all -y
sudo yum install java-11-openjdk-devel java-1.8.0-openjdk-devel -y
java -version
git --version
```

## 2. Download, extract and Install Maven
``` sh
#Step1) Download the Maven Software
sudo wget https://dlcdn.apache.org/maven/maven-3/3.8.5/binaries/apache-maven-3.8.5-bin.zip
sudo unzip apache-maven-3.8.5-bin.zip
sudo rm -rf apache-maven-3.8.5-bin.zip
sudo mv apache-maven-3.8.5/ maven
```
## .#Step3) Set Environmental Variable  - For Specific User eg ec2-user
``` sh
vi ~/.bash_profile  # and add the lines below
export M2_HOME=/opt/maven
export PATH=$PATH:$M2_HOME/bin
```
## .#Step4) Refresh the profile file and Verify if maven is running
```sh
source ~/.bashrc
mvn -version
```
## .#Step5) Copy Maven Files
``` sh

sudo scp maven-web-app.war UserName@ServerIP:/opt/Maven
Extract the files
Ranme if needed
Cd to the direcotry
Make sure Pom.xml available 
Start the build

```

## .#Step6) Change Maven Default Repository 
``` sh

Maven Default Rrepository ~/`m2/repository
Change Maven Local Repo to new local-repo /temp/MavenLocalRepo
Nano /opt/maven/config/settings.xml
Add new link to the repostiry tage under the default tag
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
  -->
  <localRepository>/New Path</localRepository>

```

## .#Step7) Maven Life cycles & commands
``` sh
There are 3 life cycles in maven.

1.Default Lifecycle
 Mvn Validate 
   It validates that the project is correct and all necessary information is available.
 Man Compile 
   It compiles the source code of the project.
 Mvn Test
   Run tests using a suitable unit testing framework. Normally if they the tests requirements fails
  then the code SHOULD NOT be packaged or deployed.
 package
  take the compiled code and package it in its distributable format, such as a JAR, WAR, EAR....
 install 
  locally. install the package into the local repository, for use as a dependency in other projects
  deploy
  projects. copies the final package to the remote repository for sharing with other developers 
  
2,Clean Lifecycle:
  clean : remove all files generated by the previous build
  Dskiptest : if we want to skip test and build
  
3,Site Lifecycle
  site generate the project's site documentation
  
  
Standalone Applications – *.jar  Java Archieve
=============================================
 java code ONLY   
    contains only java classes
    jar = .classfiles
    maven-stanalone-application.jar

Web Applications  – .war  web Archieve
======================================
Java code + 
web content (HTML, CSS, JS, images…,) 
Backend code   - frontend code
maven-web-application.war

Enterprise applications – .ear –
==================================
 Enterprise Archieve
    Multiple Modules
      Java code + web content 
    Ear =  war(s) + jar(s)
    Banking applications
    maven-web-application.war
    maven-enterprise-application.ear

===========================
What are we building? we are building java codes:
   src-- source code (raw code)
   Unit-Test-Cases 
      JAVA  --> JUnit test cases 
   buildScripts:  pom.xml


```
## Maven -Configuration directory > conf/settings.xml