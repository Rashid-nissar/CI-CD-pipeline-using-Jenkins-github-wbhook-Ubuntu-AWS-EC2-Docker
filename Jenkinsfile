pipeline {

    agent any 
    environment {
        CONTAINER_NAME ="nestjs-app"
        IMAGE_NAME ="nesths-image"
        EMAIL ="waniraashid121@gmail.com"
        PORT = "3000"
    }

    stages{

        stage('clone Repo') {
             step{
            git branch:'main', url: 
            'https://github.com/Rashid-nissar/CI-CD-pipeline-using-Jenkins-github-wbhook-Ubuntu-AWS-EC2-Docker.git' 
        }
        
         }

         stage ('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME . '
            }
         }

     stage ('stop & Remove Previous container')  {

        steps {
            sh '''
              docker stop $CONTAINER_NAME || true

              docker rm $CONTAINER_NAME || true
            '''

        }
     }
     stage ('Docker Container Run')  {

        steps {
            sh '''
              docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME

              docker rm $CONTAINER_NAME || true
            '''

        }
     }

     stage ('Send Email Notification')  {

        steps {
           emaillext(
            subject:"NestJS App Deployed Successfully on Ec2!",
            body: "your Nest JS app  is deployed! http://13.203.217.108:${PORT}/",
            to: "${EMAIL}"
           )

        }
     }
    }
}