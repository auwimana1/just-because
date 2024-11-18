pipeline{
    agent any

    parameters{
        string (name: 'DevOps' , defaultValue: '1.0.1')
    }

    stages{
        stage("build an image and push it to ecr"){
            steps{
                script{
                    // This step should not normally be used in your script. Consult the inline help for details.
                    withDockerRegistry(credentialsId: 'ecr:us-east-1:JB-Credentials', url: 'https://557195342730.dkr.ecr.us-east-1.amazonaws.com/') {

                    sh "docker build -t just-because-ecr:${params.DevOps} ."
                    sh "docker tag just-because-ecr:${params.DevOps} 557195342730.dkr.ecr.us-east-1.amazonaws.com/just-because-ecr:${params.DevOps}"
                    sh "docker tag just-because-ecr:${params.DevOps} 557195342730.dkr.ecr.us-east-1.amazonaws.com/just-because-ecr:latest"
                    sh "docker push 557195342730.dkr.ecr.us-east-1.amazonaws.com/just-because-ecr:latest"
}
                }
            }
        }
        stage("update image to ecs"){
            steps{
                    sh "aws ecs update-service --cluster Just-BEcz-Cluster --service JB-SERVICE --force-new-deployment"
            }
        }
    }
}