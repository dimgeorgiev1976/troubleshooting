# troubleshooting
kubectl logs pod/pod-name -n valkyrie-dev-86754694bf-27fwb
kubectl get events -n valkyrie-dev-86754694bf-27fwb
export valkyrie-dev=$(kubectl get pods --namespace default -l "app.kubernetes.io/component=jenkins-master" -l "app.kubernetes.io/instance=cd" -o jsonpath="{.items[0].metadata.name}") kubectl port-forward $POD_NAME 8080:8080 >> /dev/null &

https://source.cloud.google.com/qwiklabs-gcp-02-c8f9d62e13ce/valkyrie-app

If your container is in a private container respository that requires authentication, then you need to add this secret into Kubernetes and add the imagePullSecrets reference to it in your deployment.
Add the credential secret to Kubernetes
Add the reference of the secret to use in your pod definition

kubectl -namespace <YOUR NAMESPACE> \
create secret docker-registry registry-secret \
--docker-server=https://index.docker.io/v1/ \
--docker-username=<THE USERNAME> \
--docker-password=<THE PASSWORD> \
--docker-email=not-needed@example.com
  
Then add this reference so that your pod knows to use it: 
imagePullSecrets:
  - name: registry-secret
  
  /*..................................   ..................................*/
  
Change the image in the containers section of the Deployment to the following:
...
containers:
- name: auth
  image: kelseyhightower/auth:1.0.0
...

When you run the kubectl create command to create the auth deployment, it will make one pod that conforms to the data in the Deployment manifest

source/html.go 




