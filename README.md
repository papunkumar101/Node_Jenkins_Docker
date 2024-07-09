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


## Manual Jenkins Pipeline Configuration

Every time you have to create a build to deploy the latest code.

### Steps to Create a Build

1. **Click on `New Item`.**
2. **Enter the pipeline name or item name** (e.g., `pipeline-1`).
3. **Select `Freestyle project`** (it allows you to customize the pipeline more), then click `Next`.
4. **Write the description** about the pipeline.
5. **Select `Git`** for the `Source Code Management` section and provide the repository URL and branch name.
6. **Select `Execute Windows batch command`** for `Build Steps` (for Windows), and write the following command:

    ```shell
    docker rm --force node-jenkins-docker
    docker rmi --force node-jenkins-docker
    docker build -t node-jenkins-docker .
    docker run -d --name node-jenkins-docker -p 3000:3000 node-jenkins-docker
    ```

## Automation Jenkins Pipeline Configuration

Using webhooks ensures that Jenkins listens for events (like code pushes) from your repository and triggers builds automatically, reducing the need for manual intervention. This setup streamlines the CI/CD process, allowing for quicker deployments of the latest code changes.

### In Your Git Repository

1. **Go to the repository `settings`**, and find the `Webhooks` section.
2. **Add a new webhook** with the following details:
   - **Payload URL**: `http://your-jenkins-server-url/github-webhook/`
   - **Content type**: `application/json`
   - **Events**: Choose `Pull and push event`.

### In Jenkins

1. **Go to the configuration page of your Jenkins job.**
2. **In the `Build Triggers` section**, select `GitHub hook trigger for GITScm polling`.
