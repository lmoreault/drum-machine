pipeline {
    agent {
        node {
            label 'linux'
        }
    }
    tools {
        nodejs 'NodeJS9'
    }
    stages {
        stage('Build') {
            steps {
                //git 'https://github.com/lmoreault/drum-machine.git'
                sh 'npm install'
                sh 'npm run-script build'
                sh 'npm run-script test'
            } 
            post {
                always {
                    junit "tests-results/*.xml"
                }
                success {
                    archiveArtifacts 'public/**/*'
                }
            }
        }
        stage('Deploy') {
            steps {
                copyArtifacts(projectName: 'drum-machine-pipeline', target: 'build')
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Jay Dee Machine', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/', remoteDirectorySDF: false, removePrefix: 'build/public', sourceFiles: 'build/public/**/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        stage('Smoke Test') {
            steps {
                sh "curl http://localhost:8081"
            }
        }
    }
}