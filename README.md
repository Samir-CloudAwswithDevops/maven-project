# Maven Project Deployment

#### What is Maven?

Maven is a **build automation and project management tool** primarily used for Java projects. It helps developers:

- Manage project dependencies (libraries and frameworks your project needs).  
- Compile, test, and package the code automatically.  
- Define a standard project structure and lifecycle.  
- Generate documentation and reports.  
- Easily build multi-module projects.  
- Share project configurations and dependencies in a standardized way using a file called `pom.xml`.  

### Maven Goals
| Command | Description |
|---------|-------------|
| `mvn clean` | Cleans previous project run files. |
| `mvn compile` | Converts source code into machine-understandable bytecode. |
| `mvn test` | Runs test cases. |
| `mvn package` | Creates final package (`.jar`, `.war`, `.ear`) in the project repository. |
| `mvn install` | Creates the final package and installs it into the **local repository**. |

---

## EC2 Instance Setup
1. Create one EC2 instance.  
2. Choose **Instance type:** `t3.micro`.  
3. Configure **key pair**, **security group**, and **IAM role**.

---

## Installing Required Tools

```bash
sudo su -

# Install Maven
yum install maven -y
mvn --version

# Install Git
yum install git -y

#### Install Tree command###
yum install tree -y

###Example Maven version output:###
Apache Maven 3.8.4 (Red Hat 3.8.4-3.amzn2023.0.5)
Maven home: /usr/share/maven
Java version: 17.0.17, vendor: Amazon.com Inc., runtime: /usr/lib/jvm/java-17-amazon-corretto.x86_64

###Clone the Project###
bash
Copy code
git clone https://github.com/Samir-CloudAwswithDevops/maven-project.git
cd maven-project
cd maven-project <inside>#### mvn clean ####   clean all jar,war,file like fresh structre goals

               use command - tree 

output- [INFO] Scanning for projects...
[INFO] 
[INFO] ----------------------< com.mycompany.app:my-app >----------------------
[INFO] Building my-app 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ my-app ---
[INFO] Deleting /root/sample-maven-project/target
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.364 s
[INFO] Finished at: 2025-11-25T09:44:45Z
[INFO] ------------------------------------------------------------------------
[root@ip-172-31-67-117 maven-project]# tree
.
├── README.md
├── pom.xml
└── src
    ├── main
    │   └── java
    │       └── com
    │           └── mycompany
    │               └── app
    │                   └── App.java
    └── test
        └── java
            └── com
                └── mycompany
                    └── app
                        └── AppTest.java

 ##### type command- mvn compile ##### create jar,war,var file ####

output 
.
├── README.md
├── pom.xml
├── src
│   ├── main
│   │   └── java
│   │       └── com
│   │           └── mycompany
│   │               └── app
│   │                   └── App.java
│   └── test
│       └── java
│           └── com
│               └── mycompany
│                   └── app
│                       └── AppTest.java
└── target
    ├── classes
    │   └── com
    │       └── mycompany
    │           └── app
    │               └── App.class
    ├── generated-sources
    │   └── annotations
    └── maven-status
        └── maven-compiler-plugin
            └── compile
                └── default-compile
                    ├── createdFiles.lst
                    └── inputFiles.lst

 ##### mvn clean & mvn complie are build success then run command mvn test ######

output -  type command mvn test

-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running com.mycompany.app.AppTest
Tests run: 2, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.016 sec

Results :

Tests run: 2, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------

.
├── README.md
├── pom.xml
├── src
│   ├── main
│   │   └── java
│   │       └── com
│   │           └── mycompany
│   │               └── app
│   │                   └── App.java
│   └── test
│       └── java
│           └── com
│               └── mycompany
│                   └── app
│                       └── AppTest.java
└── target
    ├── classes
    │   └── com
    │       └── mycompany
    │           └── app
    │               └── App.class
    ├── generated-sources
    │   └── annotations
    ├── generated-test-sources
    │   └── test-annotations
    ├── maven-status
    │   └── maven-compiler-plugin
    │       ├── compile
    │       │   └── default-compile
    │       │       ├── createdFiles.lst
    │       │       └── inputFiles.lst
    │       └── testCompile
    │           └── default-testCompile
    │               ├── createdFiles.lst
    │               └── inputFiles.lst
    ├── surefire-reports
    │   ├── TEST-com.mycompany.app.AppTest.xml
    │   └── com.mycompany.app.AppTest.txt
    └── test-classes
        └── com
            └── mycompany
                └── app
                    └── AppTest.class

###### Generate a project with a specific archetype  install a archetype in server ##########

mvn archetype:generate \
  -DarchetypeGroupId=org.apache.maven.archetypes \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DarchetypeVersion=1.4 \
  -DgroupId=com.example \
  -DartifactId=my-app \
  -Dversion=1.0.0 \
  -DinteractiveMode=false


 #######then run this command for Interactive mode (asks for groupId, artifactId, etc.)######

          mvn archetype:generate  ----after run this command showing many groupid, artifactid like 

 
output- 
Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): 2293: 3580 👈 #choose any group id ###
Downloading from central: https://repo.maven.apache.org/maven2/top/tshare/maven/ddd-scaffold-lite-test/1.0/ddd-scaffold-lite-test-1.0.jar
Downloaded from central: https://repo.maven.apache.org/maven2/top/tshare/maven/ddd-scaffold-lite-test/1.0/ddd-scaffold-lite-test-1.0.jar (55 kB at 77 kB/s)

then choose any number like -

        Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): 2293: 3580
        Choose za.co.absa.hyperdrive:component-archetype version: 
        1: 1.0.0    👈
        2: 2.0.0    👈
        3: 3.0.0    👈
        4: 3.1.0    👈      ###choose any one  latest number###
        5: 3.2.2    👈
        6: 3.3.0    👈
        7: 4.0.0    👈
        8: 4.1.0    👈
        Choose a number: 8: 7 👉  then enter 

then showing groupId, artifactId like - Downloaded from central: https://repo.maven.apache.org/maven2/za/co/absa/hyperdrive/component-archetype/4.0.0/component-archetype-4.0.0.jar (9.7 kB at 17 kB/s)
Define value for property 'groupId': apple        ### groupid name ###
Define value for property 'artifactId': com.uber  ###  artifactid name ###
Define value for property 'version' 1.0-SNAPSHOT: ### 👉  then enter ###
Define value for property 'package' apple:        ### then check correct groupId, artifactId name  ###
Confirm properties configuration:                 👉  then enter 
groupId: apple                                     
artifactId: com.uber
version: 1.0-SNAPSHOT
package: apple
 Y:           👉  then enter              

show build failure 

then goto [root@ip-172-31-67-117 ~maven-project] ls
pom.xml com.uber src target file1

[root@ip-172-31-67-117 ~]cd com.uber

[root@ip-172-31-67-117 ~com.uber]ls
pom.xml


then type command - mvn clean

                  - mvn compile 
output can see the screenshot you uploaded (showing BUILD SUCCESS) — everything looks correct. 🎉
 

then type command - mvn test 

output 
-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running com.mycompany.app.AppTest
Tests run: 2, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.016 sec

Results :

Tests run: 2, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------

all output are there in screenshot 
