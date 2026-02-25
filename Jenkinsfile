pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                
                checkout scm
            }
        }

        stage('Validation') {
            steps {
                sh 'test -f index.html'
                echo 'Validation réussie.'
            }
        }

        stage('Deploy') {
            steps {
                withCredentials([string(credentialsId: 'ALWAYSDATA_PASSWORD', variable: 'SSH_PASS')]) {
                    
                    sh 'sshpass -p "${SSH_PASS}" scp -o StrictHostKeyChecking=no index.html devops-lab@ssh-devops-lab.alwaysdata.net:www/'
                }
            }
        }
    }
}
