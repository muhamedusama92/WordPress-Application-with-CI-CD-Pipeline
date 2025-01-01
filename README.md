# WordPress Application with CI/CD Pipeline

## Overview
This project demonstrates building and deploying a WordPress application using Docker Compose and setting up a CI/CD pipeline using Jenkins. The pipeline automates the process of testing, building, and deploying the application, ensuring a seamless development workflow.

## Features
- **Containerized WordPress Application**: Uses Docker Compose to manage WordPress and MySQL services.
- **Automated CI/CD Pipeline**: Employs Jenkins for continuous integration and deployment.
- **Master-Slave Agent Setup**: Runs the Jenkins pipeline on a master-slave architecture using the Jenkins agent JAR file.
- **Version Control**: Integrated with GitHub to track changes and trigger pipeline execution.

## Project Structure
```
.
├── docker-compose.yml       # Defines the services and networks for Docker Compose
├── Jenkinsfile              # Pipeline script for Jenkins
├── README.md                # Project documentation
└── .env                     # Environment variables for configuration (optional)
```

## Prerequisites
1. **Docker & Docker Compose**: Ensure Docker and Docker Compose are installed on your system.
2. **Jenkins**: Install and configure Jenkins with the following plugins:
   - Git
   - Pipeline
3. **GitHub Repository**: Clone or fork this repository to use as a starting point.
4. **Jenkins Master-Slave Setup**: Configure Jenkins master and slave nodes using the Jenkins agent JAR file.

## Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/muhamedusama92/WordPress-Application-with-CI-CD-Pipeline.git
cd WordPress-Application-with-CI-CD-Pipeline
```

### 2. Configure Environment Variables
Create a `.env` file to define your environment variables (optional):
```env
WORDPRESS_DB_PASSWORD=your_password
MYSQL_ROOT_PASSWORD=your_root_password
```

### 3. Start Docker Compose
Launch the WordPress and MySQL services:
```bash
docker-compose up -d
```
Access the WordPress application at `http://localhost:8000`.

### 4. Set Up Jenkins Pipeline

#### a. Create a New Jenkins Pipeline Job
1. Go to Jenkins Dashboard and create a new pipeline job.
2. Configure the pipeline to pull the `Jenkinsfile` from your repository.

#### b. Configure Master-Slave Agents
1. Set up a slave node in Jenkins by going to `Manage Jenkins > Manage Nodes and Clouds > New Node`.
2. Download the agent JAR file from the master node.
3. Run the agent on the slave node using the following command:
   ```bash
   java -jar agent.jar -jnlpUrl <JENKINS_MASTER_URL>/computer/<NODE_NAME>/slave-agent.jnlp -secret <NODE_SECRET> -workDir "<WORK_DIRECTORY>"
   ```
4. Ensure the slave node is connected and online.

#### c. Pipeline Configuration
The `Jenkinsfile` is pre-configured to:
- Pull the latest code from GitHub.
- Build Docker images.
- Deploy the application using Docker Compose.
- Execute stages on the appropriate agent.

#### d. Trigger the Pipeline
Manually build the pipeline or configure a webhook in GitHub for automated triggers on push events.

## Jenkinsfile Explained
The `Jenkinsfile` contains:
- **Stages**:
  - Checkout: Pulls the latest code.
  - Build: Builds Docker images.
  - Deploy: Deploys the application using `docker-compose`.
- **Agent Declaration**: Specifies the agent (master or slave) for each stage.
- **Steps**: Shell commands and Jenkins plugins for automation.

## Additional Notes
- **Database Persistence**: Ensure volumes are configured correctly in `docker-compose.yml` to retain data.
- **Security**: Avoid hardcoding sensitive information like passwords. Use environment variables or secrets management tools.
- **Scaling**: Consider extending the setup with Docker Swarm or Kubernetes for scalability.

## Contributing
Feel free to open issues or submit pull requests to improve this project.

