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

# Install Tree command
yum install tree -y
Example Maven version output:

yaml
Copy code
Apache Maven 3.8.4 (Red Hat 3.8.4-3.amzn2023.0.5)
Maven home: /usr/share/maven
Java version: 17.0.17, vendor: Amazon.com Inc., runtime: /usr/lib/jvm/java-17-amazon-corretto.x86_64
Clone the Project
bash
Copy code
git clone https://github.com/Samir-CloudAwswithDevops/maven-project.git
cd maven-project
ls
Maven Build Lifecycle
1. Clean Project
bash
Copy code
mvn clean
Output example:

csharp
Copy code
[INFO] BUILD SUCCESS
bash
Copy code
tree
css
Copy code
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
2. Compile Project
bash
Copy code
mvn compile
Output example:

pgsql
Copy code
target/
├── classes/
│   └── com/mycompany/app/App.class
├── generated-sources/
└── maven-status/
3. Run Tests
bash
Copy code
mvn test
Output example:

yaml
Copy code
Running com.mycompany.app.AppTest
Tests run: 2, Failures: 0, Errors: 0, Skipped: 0
[INFO] BUILD SUCCESS
Generating a Project with a Specific Archetype
bash
Copy code
mvn archetype:generate \
  -DarchetypeGroupId=org.apache.maven.archetypes \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DarchetypeVersion=1.4 \
  -DgroupId=com.example \
  -DartifactId=my-app \
  -Dversion=1.0.0 \
  -DinteractiveMode=false
Interactive Mode
bash
Copy code
mvn archetype:generate
Choose a groupId, artifactId, and version from the list.

Follow the prompts to define project properties.

Example selections:

python
Copy code
Choose a number or apply filter: 2293:3580
Choose version: 4.1.0
Define value for property 'groupId': apple
Define value for property 'artifactId': com.uber
Define value for property 'version' 1.0-SNAPSHOT: [ENTER]
Define value for property 'package' apple: [ENTER]
Confirm properties configuration: Y
After configuration, build project:

bash
Copy code
mvn clean
mvn compile
mvn test
All output should show BUILD SUCCESS.

Project Structure
swift
Copy code
.
├── pom.xml
├── src/
│   ├── main/java/com/mycompany/app/App.java
│   └── test/java/com/mycompany/app/AppTest.java
└── target/
Screenshots
BUILD SUCCESS output is visible in the terminal screenshot:
