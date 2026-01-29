//Jenkinsfile dengan scripted pipeline
// node {
//     stage('Check directory') {
//         //stage ini saya buat karena pada build sebelumnya file package.json tidak terbaca oleh Jenkins
//         checkout scm
//         sh  'git config --global --add safe.directory "*"'
//         sh  'ls -l'
//     }
//     nodejs('node-latest') {
//         //disini saya menggunakan agent nodejs dengan label 'node-latest' karena saya sudah mengkonfigurasi NodeJS tool di Jenkins
//         stage('Build') {
//             sh  'npm install'
//         }
//         stage('Test') {
//             sh  './jenkins/scripts/test.sh'
//         }
//         stage('Deploy') {
//             sh  './jenkins/scripts/deliver.sh'
//             input message:  'sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
//             sh  './jenkins/scripts/kill.sh'
//         }
//     }
// }

//declarative pipeline
pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Fix and Checkout') {
            steps {
                checkout scm
                deleteDir()
                sh "git config --global --add safe.directory /var/jenkins_home/workspace/react-app"
                
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
                sh'./jenkins/scripts/deliver.sh'
                input message:'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
                sh'./jenkins/scripts/kill.sh'
            }
        }
    }
}
