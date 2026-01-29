pipeline {
    agent {
        docker {
            image 'node:16'
            args '-p 3001:3001'  
        }
    }
    options {
        skipDefaultCheckout()  
    }
    stages {
        stage('Fix and Checkout') {
            //stage ini dibuat karena pada build sebelumnya git repository tidak terbaca oleh jenkins
            steps {
                deleteDir()  
                sh 'git config --global --add safe.directory /var/jenkins_home/workspace/react-app'  
                checkout scm  
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'  
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk melanjutkan)'

            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                sleep 60
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}