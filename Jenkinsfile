pipeline{
  agent any
  environment {
    AWS_DEFAULT_REGION = 'us-east-1'
  }
    stages{
        stage("docker"){
            steps{
                sh '''
                docker image build -t manual-awscli  .
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

        stage(ECS_IMAGE_BUILD){
            agent{
                docker{
                    image 'manual-awscli'
                    reuseNode true
                    args '-u root -v /var/run/docker.sock:/var/run/docker.sock'
                }
            }

            steps{
                withCredentials([usernamePassword(credentialsId: 'AWS', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                          docker build --target dev -t 533267431526.dkr.ecr.us-east-1.amazonaws.com/vote -f vote/Dockerfile:1.0 .
                          aws ecr get-login-password  | docker login --username AWS --password-stdin 533267431526.dkr.ecr.us-east-1.amazonaws.com
                          docker push 533267431526.dkr.ecr.us-east-1.amazonaws.com/vote -f vote/Dockerfile:1.0

}
            }
        }
    }
 
}