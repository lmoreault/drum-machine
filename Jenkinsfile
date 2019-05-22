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
            post {
                always {
                    junit "test-results/*.xml"
                }
                success {
                    archiveArtifacts 'public/**/*'
                }
            }
        }
        stage('Deploy') {
            steps {
               sh "echo edploying"
            }
        }
        stage('Smoke Test') {
            steps {
               sh "curl http://localhost:8081"
            }
        }
    }
}