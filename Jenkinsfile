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
            }
        }
        stage('B1 beta') {
            when {
                branch 'B1beta'
            }
            steps {
                echo "b1 branch beta "
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