# troubleshooting
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






