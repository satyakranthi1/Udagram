# Udagram

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client and post photos to the feed.

[![Build Status](https://travis-ci.com/satyakranthi1/Udagram.svg?branch=master)](https://travis-ci.com/satyakranthi1/Udagram)

## Setup

**You would need the following:**
* [Docker](https://docs.docker.com/install/)
* [Terraform](https://www.terraform.io/downloads.html)
* [KubeOne](https://github.com/kubermatic/kubeone#installing-kubeone)
* [AWS S3 Bucket](https://aws.amazon.com/s3/)
* [AWS RDS](https://aws.amazon.com/rds/)

## Project Structure

**Frontend**

The frontend is an angular based ionic application. It interacts with the reverse proxy which relays the requests to the backend microservices.

**User Microservice**

The user microservice handles registration and authentication of an user.

**Feed Microservice**

The feed microservice handles populating the feed with images and posting of an image.

## Docker

1. Use `docker-compose -f docker-compose-build.yaml build --parallel` to build the images using the file available under the docker folder.
2. Use `docker run --publish 8080:8080 --name [name] [dockerid/image-repo]` to run the docker images. Add environment variables needed using the flag `--env`. 

## Kubernetes

1. Use the [steps](https://github.com/kubermatic/kubeone/blob/master/docs/quickstart-aws.md) available in kubeone github repo to setup infrastructure for cluster and to install kubernetes on it.
2. Provide the necessary configs in env-configmap.yaml, env-secret.yaml and aws-secret.yaml files that are in k8s folder.
3. Use `kubectl apply -f [filename]` and apply all the files under k8s folder. This should push the containers onto the provisioned kubernetes cluster on aws.
4. Use `kubectl port-forward service/*end <locahost-port>:<pod-port>` to forward the deployment port to localhost port.
5. Test in a web browser once you forwarded both the frontend and reverseproxy.

## CI/CD
Continuous Integeration is done using Travis CI. To setup Travis CI, signin using your github account at https://travis-ci.com/ and provide access to your github repository. Add a travis.yaml file at the root of your github repository. Configure your environment variables and build triggers. You can encrypt your environment variables using [travisci-cli](https://github.com/travis-ci/travis.rb#readme).
