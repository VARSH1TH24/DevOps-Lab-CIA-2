**Course Registration System — DevOps Assessment**



1\. Project Overview



This project implements a Java-based Course Registration System. It validates course registration using course capacity, course activity, prerequisites, duplicate registration checks, and the maximum permitted credit limit.



2\. Technologies Used



\- Java 17

\- Maven

\- JUnit 5

\- Git and GitHub

\- Jenkins Declarative Pipeline

\- Docker

\- Kubernetes

\- Minikube

\- Nginx



3\. Git Workflow



Development was performed on the feature branch `feature/course-registration`.



The work includes:

\- Fixing the course capacity boundary condition.

\- Adding registration boundary tests.

\- Updating the maximum permitted registered credits from 20 to 24.

\- Restructuring the project as a Maven multi-module build.

\- Adding a Jenkins Declarative Pipeline.

\- Adding Kubernetes Deployment and NodePort Service manifests.



4\. Maven Multi-Module Structure



Student-Starter/

├── pom.xml

├── Jenkinsfile

├── deployment.yaml

├── service.yaml

├── README.md

└── course-registration-app/

&#x20;   ├── pom.xml

&#x20;   └── src/

&#x20;       ├── main/java/com/university/

&#x20;       │   ├── Course.java

&#x20;       │   ├── RegistrationService.java

&#x20;       │   └── Student.java

&#x20;       └── test/java/com/university/

&#x20;           ├── CourseTest.java

&#x20;           └── RegistrationServiceTest.java





The root POM acts as the parent project and manages the child module, Java version, JUnit dependency version, and Maven plugin versions.



5\. Build and Test



Run the following commands from the project root:



mvn clean test

mvn package



JUnit reports are generated under:



`course-registration-app/target/surefire-reports/`



The packaged JAR is generated under:



`course-registration-app/target/`



6\. Jenkins CI Pipeline



The root `Jenkinsfile` defines a Declarative Pipeline with these stages:



1\. Build and Test — executes `mvn clean test`.

2\. Package — executes `mvn package`.



The pipeline publishes JUnit test results and archives the generated JAR. Windows agents use the `bat` command.



7\. Kubernetes Deployment



The Kubernetes configuration uses the `nginx:1.27` container image.



\- Deployment: `nginx-deployment`

\- Initial replicas: 2

\- Service: `nginx-service`

\- Service type: NodePort

\- Container port: 80

\- NodePort: 30080



Apply the configuration:





kubectl apply -f deployment.yaml

kubectl apply -f service.yaml





Verify the resources:





kubectl get deployments

kubectl get pods

kubectl get services





\## 8. Scaling and Self-Healing



Scale the Deployment to three replicas:





kubectl scale deployment nginx-deployment --replicas=3

kubectl get deployments

kubectl get pods





Delete one of the Deployment-managed Pods to demonstrate self-healing:





kubectl delete pod <POD\_NAME>

kubectl get pods -w





Replace `<POD\_NAME>` with the name of an actual Nginx Pod. Kubernetes creates a replacement Pod to maintain the desired replica count.



9\. Service Verification



Access the Nginx service with:





minikube service nginx-service --url





The Nginx welcome page confirms that the web server is reachable through the exposed service.



10\. Assessment Evidence



Captured genuine screenshots of the following:



1\. Git branch and commit history.

2\. Successful `mvn clean test` output.

3\. Successful `mvn package` output and generated JAR.

4\. Jenkinsfile and, if executed, the Jenkins build results.

5\. Kubernetes Deployment, Pods, and NodePort Service.

6\. Three available replicas after scaling.

7\. Pod deletion and replacement demonstrating self-healing.

8\. Nginx welcome page in the browser.



Note: A configured Jenkinsfile alone does not establish that a Jenkins build has run. Include a Jenkins execution screenshot only if an actual build was performed.

