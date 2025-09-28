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
                withCredentials([sshUserPrivateKey(credentialsId: 'AppVM', keyFileVariable: 'SSH_Access')]) {
                    sh '''
                    #Install httpd Server
                    ssh -i "$SSH_Access" ec2-user@13.201.127.99 "sudo dnf install httpd -y"
                    ssh -i "$SSH_Access" ec2-user@13.201.127.99 "sudo systemctl restart httpd"
                    '''
                }
            }
        }
    }
}
