pipeline {
    agent any
    stages {
        stage('Debug Info') {
            steps {
                sh 'export PATH=$PATH:/usr/local/bin && which docker && docker --version && whoami'
            }
        }
        stage('Clean Up') {
            steps {
                sh 'export PATH=$PATH:/usr/local/bin && docker rm -f hello-devops 2>/dev/null || echo "Container not found or already removed."'
            }
        }
        stage('Build') {
            steps {
                sh 'export PATH=$PATH:/usr/local/bin && docker build -t hello-devops .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'export PATH=$PATH:/usr/local/bin && docker run -d --name hello-devops -p 5001:5001 hello-devops'
            }
        }
    }
}
