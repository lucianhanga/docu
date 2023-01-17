# Continous Integration/Continous Deployment

## CI/CD on AWS

---

- **step 1.** - Create a local Docker Image
- **step 2.** - on AWS create a `ECR (Elastic Container Repository)` for storing Docker images for application(s)
- **step 3.** - Tag the local image with the ECR `ARN - Amazon Resource Name`
- **step 4.** - give the docker CLI access to access the AWS account
- **step 5.** - push the docker image to ECR
- **step 6.** - in `ECS - Elastic Container Service` create the `ECS Cluster`, `ECS Task`, `ECS Serivce` - using the docker image
- **step 7.** - export the `ECS Task` as `json` - will be needed for the deployment automation

Build up the Continous Integration Pipeline 

- **step 8.** - define an test action: `.github/workflows/test.yml`. Check out: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

Build up the Deployment Pipeline with GitHub Actions/workflows

- **step 9.** - add the  `ECS Task json` to the project
- **step 10.** - select the project on the `github` webpage, choose `Deploy to Amazon ECS` and make the appropriate changes in the the `.github/workflows/aws.yml` which is create automatically.
- **step 11.** - when changes are commited to the selected branch the deployment will be initiated.

## CI/CD on Jenkins and Jest (and react testing library)

---

Jenkins controler:

**Freestyle Jobs** - chained using `build triggers`

- it always restars from beginning when it was stopped

**Pipeline** - defined through `Jenkinsfile`

- this can be stoped and then starte from teh point where it was stopped

**Blue Ocean** - ...


- **step 1.** - Check out the code from source control
- **step 2.** - NPM install and npm run build (front-end)
- **step 3.** - npm test
- **step 4.** - Docker build + publish
- **step 5.** - Deploy app
- **step 6.** - Bump version
- **step 7.** - Git push
- **step 8.** - Docker cleanup
