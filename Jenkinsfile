pipeline {
    agent { 
        kubernetes{
            label 'jenkins-slave'
        }
    }
        
     options {
        skipStagesAfterUnstable()
    }
environment 
    {
        PROJECT = 'mb-eye:latest'
        ECRURL = 'https://633706706076.dkr.ecr.us-east-1.amazonaws.com'
        ECRCRED = 'ecr:us-east-1:aws-main-admin-user'
        DOCKER_CONFIG = "/home/ec2-user/.docker/config.json"
    }

stages { 
    stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
    }   
    
    stage('Docker image pull'){
        steps{
            script{
                    sh '''
                    
                        eval $(aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 633706706076.dkr.ecr.us-east-1.amazonaws.com | sed 's|https://||')
                       
                       '''
                    docker.withRegistry(ECRURL, ECRCRED)
                    {
                        docker.image(PROJECT).pull()
                    }
                }
            }
        }

    stage('deploy') {
        steps{
            sh script:
            '''
            curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
            chmod +x ./kubectl
            ./kubectl apply -f mb-eye-deployment.yml
            ./kubectl apply -f mb-eye-services.yml
            
            '''
        }
    }
    }
}    

