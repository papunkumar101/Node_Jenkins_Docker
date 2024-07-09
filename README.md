# Node_Jenkins_Docker

Creating a Jenkins Freestyle project for a Node.js application using Docker involves configuring the Source Code Management to pull from a Git repository and defining build steps using Windows batch commands.


## Server Requirements

- Node.js
- Docker
- Jenkins

## Installation

1. Clone the project.
2. Run the following command in CMD:

   ```sh
   node index.js


## Manuall Jenkins Pipeline Configuration : 
Every time you have to create build to deploy latest code.
Steps1: Click on `New Item``.
Steps2: Enter the pipeline name or item name (Ex: pipeline-1)
Steps3: Select `Freestyle project` (it allow you to more customization for the pipeline), Next
Steps4: Write the Description about the pipeline
Steps5: Select `Git` for `Source Code Management` section provide the repo url and branch name.
Steps6: Select `Execute window batch command` for `Build Steps` (for window), write the bellow command: 

docker rm --force node-jenkins-docker
docker rmi --force node-jenkins-docker
docker build -t node-jenkins-docker .
docker run -d --name node-jenkins-docker -p 3000:3000 node-jenkins-docker


## Automation Jenkins Pipeline Configuration : 
Using webhooks ensures that Jenkins listens for events (like code pushes) from your repository and triggers builds automatically, reducing the need for manual intervention. This setup streamlines the CI/CD process, allowing for quicker deployments of the latest code changes.
### In Your Git Repository:
Step1: Go to the repository `settings`, Find the `Webhooks` section.
Step2: Add a new webhook with the following details:
        Payload URL(http://your-jenkins-server-url/github-webhook/)
        Content type(application/json)
        Events(Choose Just the push event.)
### In Jenkins:
Step1: Go to the configuration page of your Jenkins job.
Step2: In the `Build Triggers` section, select `GitHub hook trigger for GITScm polling`.