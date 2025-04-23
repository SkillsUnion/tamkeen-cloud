## Automating Docker Deployment with CodeBuild and CodePipeline

### Step 1: Create `buildspec.yml` in Project Root
```yaml
version: 0.2
phases:
  pre_build:
    commands:
      - echo Logging in to Amazon ECR...
      - aws ecr get-login-password | docker login --username AWS --password-stdin <account_id>.dkr.ecr.<region>.amazonaws.com
      - IMAGE_TAG=$(echo $CODEBUILD_RESOLVED_SOURCE_VERSION | cut -c 1-7)
      - REPOSITORY_URI=<account_id>.dkr.ecr.<region>.amazonaws.com/my-node-app
  build:
    commands:
      - docker build -t $REPOSITORY_URI:$IMAGE_TAG .
  post_build:
    commands:
      - docker push $REPOSITORY_URI:$IMAGE_TAG
      - printf '[{"name":"app","imageUri":"%s"}]' $REPOSITORY_URI:$IMAGE_TAG > imagedefinitions.json
artifacts:
  files:
    - imagedefinitions.json
```

### Step 2: Create a CodeBuild Project
```bash
aws codebuild create-project \
  --name nodejs-build-project \
  --source type=CODECOMMIT,location=nodejs-ci-app \
  --artifacts type=CODEPIPELINE \
  --environment type=LINUX_CONTAINER,image=aws/codebuild/standard:7.0,computeType=BUILD_GENERAL1_SMALL \
  --service-role arn:aws:iam::<account_id>:role/codebuild-role
```

### Step 3: Create CodePipeline Definition (pipeline.json)
```json
{
  "pipeline": {
    "name": "NodejsContainerPipeline",
    "roleArn": "arn:aws:iam::<account_id>:role/codepipeline-role",
    "artifactStore": {
      "type": "S3",
      "location": "<your-s3-artifact-bucket>"
    },
    "stages": [
      {
        "name": "Source",
        "actions": [
          {
            "name": "SourceAction",
            "actionTypeId": {
              "category": "Source",
              "owner": "AWS",
              "provider": "CodeCommit",
              "version": "1"
            },
            "outputArtifacts": [ { "name": "SourceOutput" } ],
            "configuration": {
              "RepositoryName": "nodejs-ci-app",
              "BranchName": "main"
            }
          }
        ]
      },
      {
        "name": "Build",
        "actions": [
          {
            "name": "BuildDockerImage",
            "actionTypeId": {
              "category": "Build",
              "owner": "AWS",
              "provider": "CodeBuild",
              "version": "1"
            },
            "inputArtifacts": [ { "name": "SourceOutput" } ],
            "outputArtifacts": [ { "name": "BuildOutput" } ],
            "configuration": {
              "ProjectName": "nodejs-build-project"
            }
          }
        ]
      }
    ],
    "version": 1
  }
}
```

### Step 4: Create Pipeline
```bash
aws codepipeline create-pipeline --cli-input-json file://pipeline.json
```

---

## Result
You now have a fully automated pipeline that builds and pushes Docker images to ECR whenever code is committed to your repository. This workflow can be extended to include ECS or EKS deployment stages.