pipeline {
    agent any
    environment {
        remote_dir = "/opt/hello"
    }
    triggers{
        gitlab( triggerOnPush: true,
                triggerOnMergeRequest: true,
                branchFilterType: 'All',
                secretToken: "${env.git_token}")
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
        timestamps()
    }
    stages {
        stage('部署到测试环境'){
            when {
                branch 'test'
            }
            steps{
                sh '''
                    rsync -avz --progress -e 'ssh -p 22' --exclude='Jenkinsfile' --exclude='.git' --delete ${WORKSPACE}/  root@192.168.3.68:$remote_dir
                '''
            }
        }
        stage('部署到线上环境') {
            when {
                branch 'master'
            }
            steps {
                sh '''
                    rsync -avz --progress -e 'ssh -p 22' --exclude='Jenkinsfile' --exclude='.git' --delete ${WORKSPACE}/  root@192.168.3.61:$remote_dir
                '''
            }
        }
        stage('delete') {
            steps {
                echo '清理工作目录'
                cleanWs()
            }
        }
    }
    post {
        success {
            sh "echo 成功了"
        }
        failure {
            sh "echo 失败了"
        }
    }
}