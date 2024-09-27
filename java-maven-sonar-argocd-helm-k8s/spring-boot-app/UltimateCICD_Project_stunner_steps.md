1. First Install the jenkins on your VM, and configure the required extensions onto Jenkins.
2. Add required credentials like Docker, sonarqube and Github
3. Create a Pipeline and code via repo available there, add required repo link and credentials.
4. Install Sonarqube on the VM
5. follow the url https://github.com/Stunner59/Jenkins_SarveshXAbhishek/blob/main/java-maven-sonar-argocd-helm-k8s/spring-boot-app/README.md
6. install mvn packages using mvn clean package
7. then edit the jenkinsfile, docker agent, change the sonarqube url, change the docker repository, change username and repo.
8. Before running the jenkins job run the command in VM  ```sudo usermod -a -G docker $USER```
9. The Docker image gets updated with the BUILD_NUMBER of the jenkins job as the tag.

```
This line updates the tag number of the docker image every time there in a new build started.
 sed -i "s/replaceImageTag/${BUILD_NUMBER}/g" java-maven-sonar-argocd-helm-k8s/spring-boot-app-manifests/deployment.yml
                    
// Purpose: This command uses the sed tool to perform an in-place replacement in the deployment.yml file.
// Action: It searches for the placeholder replaceImageTag in the deployment.yml file located at java-maven-sonar-argocd-helm-k8s/spring-boot-app-manifests/.
// Replacement: It replaces replaceImageTag with the value of the BUILD_NUMBER variable throughout the file. This typically updates the image tag of the container in the Kubernetes deployment to a new version represented by BUILD_NUMBER.
// BUILD NUMBER is the current build of jenkins pipeline.

```

10. Install ArgoCD in Kubernetes Cluster either using Helm Charts or Operators.
```
https://operatorhub.io/operator/argocd-operator
```
11. password will be at location
```
kubectl get secret example-argocd-cluster -o jsonpath='{.data.admin\.password}' | base64 --decode
```

12. create a new task, add the git repo link, add the manifest file location, and sync it on auto mode.
13. It will continously monitor the git manifest folder and will deploy it on Cluster if any changes are made on github. 
