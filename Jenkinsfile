 pipeline {
    agent any
    environment {
        remote_dir = "/opt/hello"
    }
    stages {
        stage('test master'){
            when {
                branch 'master'
            }
            steps{
                echo "master branch event"
            }
        }
        stage('test B1') {
            when {
                branch 'B1'
            }
            steps {
                echo "b1 branch "
                sh 'env'
                sh 'git tag -l'
                script {
                    tag = 'v06'
                    //tag = sh (
                    //script: 'git describe --tags --abbrev=0',
                    //returnStdout: true
                    //).trim()
                    }
            }
        }
        stage('test B1 v06') {
            when {
                tag 'v06'
            }
            steps {
                echo "b1 branch  v06 "
            }
        }
    }
    post {
        success {
            sh "echo ok"
        }
        failure {
            sh "echo failure"
        }
    }
}