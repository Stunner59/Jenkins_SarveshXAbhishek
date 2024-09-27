# Spring Boot based Java web application
 
This is a simple Sprint Boot based Java application that can be built using Maven. Sprint Boot dependencies are handled using the pom.xml 
at the root directory of the repository.

This is a MVC architecture based application where controller returns a page with title and message attributes to the view.

## Execute the application locally and access it using your browser

Checkout the repo and move to the directory

```
git clone https://github.com/iam-veeramalla/Jenkins-Zero-To-Hero/java-maven-sonar-argocd-helm-k8s/sprint-boot-app
cd java-maven-sonar-argocd-helm-k8s/sprint-boot-app
```

Execute the Maven targets to generate the artifacts

```
mvn clean package
```

The above maven target stroes the artifacts to the `target` directory. You can either execute the artifact on your local machine
(or) run it as a Docker container.

** Note: To avoid issues with local setup, Java versions and other dependencies, I would recommend the docker way. **


### Execute locally (Java 11 needed) and access the application on http://localhost:8080

```
java -jar target/spring-boot-web.jar
```

### The Docker way

Build the Docker Image

```
docker build -t ultimate-cicd-pipeline:v1 .
```

```
docker run -d -p 8010:8080 -t ultimate-cicd-pipeline:v1
```

Hurray !! Access the application on `http://<ip-address>:8010`


## Next Steps

### Configure a Sonar Server locally

```
sudo su 
apt install unzip
adduser sonarqube
sudo su - sonarqube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip
unzip *
chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424
chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424
cd sonarqube-9.4.0.54424/bin/linux-x86-64/
sudo apt-get update && sudo apt-get upgrade -y
./sonar.sh start
```

Hurray !! Now you can access the `SonarQube Server` on `http://<ip-address>:9000` 


To automatically update the image in the manifest folder we use
```
sed -i "s/replaceImageTag/${BUILD_NUMBER}/g" java-maven-sonar-argocd-helm-k8s/spring-boot-app-manifests/deployment.yml
                    
// Purpose: This command uses the sed tool to perform an in-place replacement in the deployment.yml file.
// Action: It searches for the placeholder replaceImageTag in the deployment.yml file located at java-maven-sonar-argocd-helm-k8s/spring-boot-app-manifests/.
// Replacement: It replaces replaceImageTag with the value of the BUILD_NUMBER variable throughout the file. This typically updates the image tag of the container in the Kubernetes deployment to a new version represented by BUILD_NUMBER.
// BUILD NUMBER is the current build of jenkins pipeline.
```


