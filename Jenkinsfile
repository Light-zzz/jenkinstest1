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
    }
}
