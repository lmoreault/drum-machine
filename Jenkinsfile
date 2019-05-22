pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git 'https://github.com/lmoreault/drum-machine.git'
                sh 'npm install'
                sh 'npm run-script build'
                sh 'npm run-script test'
            } 
        }
        stage('Deploy') {
            steps {
               sh "cp -r public sites"
               sh "docker cp sites student1:/"
            }
        }
        stage('Smoke Test') {
            steps {
               sh "curl http://localhost:8081"
            }
        }
    }
}