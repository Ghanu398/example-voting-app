pipeline{
  agent any
    stages{
        stage("docker"){
            steps{
                sh '''
                docker image -t manual-awscli build .
                '''
            }
        }
    }
 
}