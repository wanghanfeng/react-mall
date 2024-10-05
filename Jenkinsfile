pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/wanghanfeng/react-mall.git'
            }
        }
        stage('Build Project') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Deploy to Nginx') {
            steps {
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'remote-server',
                            transfers: [
                                sshTransfer(
                                    sourceFiles: 'build/**/*',
                                    remoteDirectory: '/usr/share/nginx/html',
                                    removePrefix: 'build',
                                    execCommand: 'docker exec my-nginx nginx -s reload'
                                )
                            ]
                        )
                    ]
                )
            }
        }
    }
}