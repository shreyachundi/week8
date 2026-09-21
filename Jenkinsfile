pipeline {
    agent any

    environment {
        PATH = "/Applications/Docker.app/Contents/Resources/bin:/usr/local/bin:/opt/homebrew/bin:${env.PATH}"
    }

    stages {

        stage('Check Docker') {
            steps {
                sh '''
                    which docker
                    docker --version
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker rm -f mycontainer || true'
                sh 'docker run -d -p 5003:5003 --name mycontainer myapp'
            }
        }
    }

    post {
        success {
            echo 'Build and run completed successfully'
        }

        failure {
            echo 'Failed building'
        }
    }
}
