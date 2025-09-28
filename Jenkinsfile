pipeline {
    agent any

    stages {
        stage('Checking') {
            steps {
                checkout scm
                sh '''
                    pwd
                    ls -ltr
                '''
            }
        }
        stage('Application steps'){
            steps{
                withCredentials([sshUserPrivateKey(credentialsId: 'f7c80b23-ded0-4b70-9cf8-1a105c6f942f', keyFileVariable: 'AppVM')]) {
                    sh '''
                    #Install httpd Server
                    ssh -i "$AppVM" ec2-user@13.201.127.99 "sudo dnf install httpd -y"
                    ssh -i "$AppVM" ec2-user@13.201.127.99 "sudo systemctl restart httpd"
                    '''
                }
            }
        }
    }
}
