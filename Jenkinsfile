pipeline{
  agent any
    stages{
        stage("docker"){
            steps{
                sh '''
                docker image -t manual-awscli build .
                '''
            }
            post {
                success{
                    sh 'echo created the images sucessfully'
                }
                failure {
                    sh 'echo some error has occured while creating the image'
                }
            }
        }
    }
 
}