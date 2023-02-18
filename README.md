# Python application to deploy on kubernetes cluster using CI/CD jenkins pipeline

## Steps:

### Create jenkins credentials:
- Create a username and password Credential for your Dockerhub account.
- Create a SecretFile Credintial for the created cluster service account.

### Create jenkins pipeline script: 
- CI stage: 
1- Build the image
2- Use Dockerhub credentials to login
3- Push the image to Dockerhub
- CD stage:
1- Activate service account
2- Connect to the cluster
3- Apply kubernetes files to deploy the application

### Create Dockerfile for the application

### Create Jenkins pipeline

### Create a webhook to trigger the pipeline on push