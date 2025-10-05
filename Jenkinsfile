pipeline {
    agent { label 'slave2' }

    stages {
        stage('Install Git & Python') {
            steps {
                sh '''
                    sudo yum install git -y
                    sudo yum install python3 -y
                    sudo yum install python3-pip -y
                    git --version
                '''
            }
        }

        stage('Checking') {
            steps {
                checkout scm
                sh '''
                    pwd
                    whoami
                    hostname -i
                    ls
                '''
            }
        }
        stage('RUN PYTHON') {
            steps {
                sh '''
                mkdir /opt/test12/
                sudo cp /home/ec2-user/dipesh/workspace/Jobs/job3/sample.py /opt/test12/sample.py
                sudo cp /home/ec2-user/dipesh/workspace/Jobs/job3/required.txt /opt/test12/required.txt
                cd /opt/test12/
                pip3 install -r required.txt
                nohup python3 sample.py > sample 2>&1 &
                '''
            }
        }

        // Uncomment and use this when ready
        // stage('Application steps') {
        //     steps {
        //         withCredentials([sshUserPrivateKey(credentialsId: 'slave2', keyFileVariable: 'AppVM')]) {
        //             sh '''
        //                 ssh -i "$AppVM" -o StrictHostKeyChecking=no ec2-user@13.233.7.131 "sudo dnf install httpd -y && sudo systemctl start httpd"
        //                 scp -i "$AppVM" -o StrictHostKeyChecking=no index.html netflixstyles.css scripts.js styles.css ec2-user@13.233.7.131:/tmp/
        //                 ssh -i "$AppVM" -o StrictHostKeyChecking=no ec2-user@13.233.7.131 "sudo mv /tmp/*.html /var/www/html/"
        //                 ssh -i "$AppVM" -o StrictHostKeyChecking=no ec2-user@13.233.7.131 "sudo mv /tmp/*.css /var/www/html/"
        //                 ssh -i "$AppVM" -o StrictHostKeyChecking=no ec2-user@13.233.7.131 "sudo mv /tmp/*.js /var/www/html/"
        //                 ssh -i "$AppVM" -o StrictHostKeyChecking=no ec2-user@13.233.7.131 "sudo systemctl restart httpd"
        //             '''
        //         }
        //     }
        // }
    }
}
