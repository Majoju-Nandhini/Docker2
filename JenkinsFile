pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Docker Image...'
                bat '''
                    docker build -t formappnew .
                '''
            }
        }

        stage('Run') {
            steps {
                echo 'Running application in Docker container...'
                bat '''
                    docker stop mycontainer || exit 0
                    docker rm mycontainer || exit 0
                    docker run -d -p 5000:5000 --name mycontainer formappnew
                '''
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
        success {
            echo 'Pipeline executed successfully.'
        }
    }
}

