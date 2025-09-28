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

        stage('Application steps') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'f7c80b23-ded0-4b70-9cf8-1a105c6f942f', keyFileVariable: 'AppVM')]) {
                    sh '''
                        #Install httpd Server
                        ssh -i "$AppVM" -o StrictHostKeyChecking=no ec2-user@13.201.127.99 "sudo dnf install httpd -y"
                        
                        #Copy Multiple Files from Git
                        scp -i "$AppVM" -o StrictHostKeyChecking=no index.html netflixstyles.css scripts.js styles.css ec2-user@13.201.127.99:/tmp/

                        #Move tmp files and paste to html directory
                        ssh -i "$AppVM" -o StrictHostKeyChecking=no ec2-user@13.201.127.99 "sudo mv /tmp/index.html /var/www/html/index.html"
                        ssh -i "$AppVM" -o StrictHostKeyChecking=no ec2-user@13.201.127.99 "sudo mv /tmp/netflixstyles.css /var/www/html/netflixstyles.css"
                        ssh -i "$AppVM" -o StrictHostKeyChecking=no ec2-user@13.201.127.99 "sudo mv /tmp/scripts.js /var/www/html/scripts.js"
                        ssh -i "$AppVM" -o StrictHostKeyChecking=no ec2-user@13.201.127.99 "sudo mv /tmp/styles.css /var/www/html/styles.css"
                        
                        #Restart the httpd server
                        ssh -i "$AppVM" -o StrictHostKeyChecking=no ec2-user@13.201.127.99 "sudo systemctl restart httpd""
                    '''
                }
            }
        }
    }
}
