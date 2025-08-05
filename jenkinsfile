pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t jenkins-demo .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add test commands if needed
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying container...'
                sh 'docker run -d -p 3000:3000 jenkins-demo'
            }
        }
    }
}
