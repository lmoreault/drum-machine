pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git 'https://bitbucket.org/webergregoire/drum-machine.git'
                sh 'npm install'
                sh 'npm run-script build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm run-script test'
            }
        }
    }
}