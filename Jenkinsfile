node {
    stage('Preparation') {
        sh  'ls -l'
    }
    nodejs('node-latest') {
        stage('Build') {
            sh  'npm install'
        }
        stage('Test') {
            sh  './jenkins/scripts/test.sh'
        }
    }
}