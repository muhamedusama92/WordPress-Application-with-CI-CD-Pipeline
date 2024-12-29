pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'wordpress-app'
    }
    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                git branch: 'master', url: 'https://github.com/your-repo/wordpress.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'docker run --rm $DOCKER_IMAGE php /path/to/test/script.php'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh '''
                docker-compose down
                docker-compose up -d
                '''
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
