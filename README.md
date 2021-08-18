# Docker-node-serverless

Docker-powered build/deployment environment for Serverless projects. This Docker image is intended for use with [Bitbucket Pipelines](https://bitbucket.org/product/features/pipelines) and [AWS CodeBuild](https://aws.amazon.com/codebuild).

See [serverless-node-dynamodb-api](https://github.com/jch254/serverless-node-dynamodb-api) for an example of this image in action.

---

This image is based on node:12-alpine ([AWS Lambda uses Node v12.x](http://docs.aws.amazon.com/lambda/latest/dg/current-supported-versions.html)) and has the AWS CLI, Serverless v2.16.0 and npm installed.

To deploy a Serverless service to AWS you will need to create an IAM user with the required permissions and set credentials. I'm setting credentials using [Bitbucket Pipelines environment variables](https://confluence.atlassian.com/bitbucket/environment-variables-in-bitbucket-pipelines-794502608.html); however setting credentials in Dockerfile is also possible.

# Install commands

Use the following steps to authenticate and push an image to your repository. For additional registry authentication methods, including the Amazon ECR credential helper, see [Registry Authentication](http://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html#registry_auth) .

1. Retrieve an authentication token and authenticate your Docker client to your registry.
    Use the AWS CLI:

```
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 923195502435.dkr.ecr.us-east-1.amazonaws.com
```

Note: If you receive an error using the AWS CLI, make sure that you have the latest version of the AWS CLI and Docker installed.

1. Build your Docker image using the following command. For information on building a Docker file from scratch see the instructions [here](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html). You can skip this step if your image is already built:

```
docker build -t docker-node-serverless .
```

1. After the build completes, tag your image so you can push the image to this repository:

```
docker tag docker-node-serverless:latest 923195502435.dkr.ecr.us-east-1.amazonaws.com/docker-node-serverless:latest
```

1. Run the following command to push this image to your newly created AWS repository:

```
docker push 923195502435.dkr.ecr.us-east-1.amazonaws.com/docker-node-serverless:latest
```

