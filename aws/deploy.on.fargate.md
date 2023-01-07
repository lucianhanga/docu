
reference: 
https://towardsdatascience.com/deploying-a-docker-container-with-ecs-and-fargate-7b0cbc9cd608



```bash
aws configure
```

# Deploying a Docker Container to ECS

## Step 1 - Create the Docker image
---

e.g.
```
$ git clone https://github.com/prakhar1989/docker-curriculum.git
$ cd docker-curriculum/flask-app
```
Create the Docker image:
```
docker build -t myapp .
```
Test the app to make sure everything is working. The flask app we downloaded listens on port 5000 so we will use the same port to test.

```
docker run --publish 5000:5000 myapp
```

## Step 2 - Create an ECR repository to store your images
---

```
aws ecr create-repository --repository-name lh-ecr-repo --region eu-central-1
```

result

```json
{
    "repository": {
        "repositoryArn": "arn:aws:ecr:eu-central-1:994966562727:repository/lh-ecr-repo",
        "registryId": "994966562727",
        "repositoryName": "lh-ecr-repo",
        "repositoryUri": "994966562727.dkr.ecr.eu-central-1.amazonaws.com/lh-ecr-repo",
        "createdAt": "2023-01-06T15:28:23+01:00",
        "imageTagMutability": "MUTABLE",
        "imageScanningConfiguration": {
            "scanOnPush": false
        },
        "encryptionConfiguration": {
            "encryptionType": "AES256"
        }
    }
}
```

list all images:
```bash
aws ecr list-images --repository-name lh-ecr-repo
```

output:

```
{
    "imageIds": []
}
```

## Step 3 - Tag the image
---

tag the local image:
```bash
docker tag python-docker 994966562727.dkr.ecr.eu-central-1.amazonaws.com/lh-ecr-repo
```

## Step 4 - Give the Docker CLI permission to access your Amazon account
---

authenticate to ECR

```bash
docker login -u AWS -p $(aws ecr get-login-password --region eu-central-1) 994966562727.dkr.ecr.eu-central-1.amazonaws.com
```

output:

```
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
Login Succeeded
```

## Step 5 - Upload your docker image to ECR
---


```bash
docker push 994966562727.dkr.ecr.eu-central-1.amazonaws.com/lh-ecr-repo
```

## Step6 - Create Cluster for ECS to use for the deployment of your container
---

##  Step 7 - Create an ECS Task
---

## Step 8 - Run the ECS Task!
---


