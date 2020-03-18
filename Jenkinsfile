 pipeline {
    agent any
    environment {
        remote_dir = "/opt/hello"
    }
    stages {
        stage('pull code'){
            steps{
                git credentialsId: 'a8a03def-7c5a-4cea-b38e-4efc58052fc5', url: 'https://github.com/AlexFengCisco/Rancher_Pipeline_01.git'
            }
        }
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
                echo "b1  branch "
                sh 'env'
                sh 'git describe --tags --abbrev=0'
                //echo $BUILD_TAG
                script {
                    //tag = 'v06'
                    tag = sh (
                    script: 'git describe --tags --abbrev=0',
                    returnStdout: true
                    ).trim()
                    }
            }
        }
        stage('test B1 v06') {
            when {
                tag 'v04'
            }
            steps {
                echo "b1 branch  v04 "
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