//declarative pipeline
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
            steps {
                deleteDir()  
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
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
