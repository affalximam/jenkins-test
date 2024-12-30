pipeline {
    agent {
        docker {
            image 'node:16-buster-slim' 
            args '-p 1234:1234' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install'
            }
        }
        stage('Test') { 
            steps {
                sh "chmod +x -R ${env.WORKSPACE}"
                sh './jenkins/scripts/test.sh' 
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message : 'Jika sudah berhasil menjalankan klik "PROCEED" untuk menahiri'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
