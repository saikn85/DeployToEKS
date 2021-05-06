# Deploying a Flask API to Amazon AWS using EKS

# External IP
[a1e1dc88023fe4e9eaf5c360ae907eea-1548071041.ap-south-1.elb.amazonaws.com](a1e1dc88023fe4e9eaf5c360ae907eea-1548071041.ap-south-1.elb.amazonaws.com)


In this project focuses on containerizing and deploying a Flask API to a Kubernetes cluster using Docker, AWS EKS, CodePipeline, and CodeBuild.

The Flask app that will be used for this project consists of a simple API with three endpoints:

- `GET '/'`: This is a simple health check, which returns the response 'Healthy'. 
- `POST '/auth'`: This takes a email and password as json arguments and returns a JWT based on a custom secret.
- `GET '/contents'`: This requires a valid JWT, and returns the un-encrpyted contents of that token. 

The app relies on a secret set as the environment variable `JWT_SECRET` to produce a JWT. The built-in Flask server is adequate for local development, but not production, so you will be using the production-ready [Gunicorn](https://gunicorn.org/) server when deploying the app.

## Project Steps

Completing the project involves several steps:

1. Writing a Dockerfile for a simple Flask API
2. Build and test the container locally
3. Create an EKS cluster
4. Store a secret using AWS Parameter Store
5. Create a CodePipeline pipeline triggered by GitHub checkins
6. Create a CodeBuild stage which will build, test, and deploy your code

### Notes

1. Build is successful when the code is error free
2. Build fails, where one of the defined test cases fails
