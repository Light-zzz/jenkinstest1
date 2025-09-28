pipeline{
  agent any
  stages{
    stage('Checking')
    steps{
      checking SCM
      sh '''
      sudo su -
      pwd
      ls -ltr
      '''
    }
  }
}
