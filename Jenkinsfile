pipeline {

    environment{
      REGISTRY = "raniamidaoui"
      IMAGE_NAME = "devops-lab-go-app"
      IMAGE_VERSION = "latest"
      REGISTRY_CRED = "docker_creds"
    }

    tools {
      go 'go_114'
    }

    agent any
    
    stages {

        stage("Build"){
            steps {
                echo "Docker Build"
                script{
                    dockerImg = docker.build("${REGISTRY}/${IMAGE_NAME}:${IMAGE_VERSION}", ".") 
                }
            }
            post{
                success{
                    echo "Build Successful"
                }
                failure{
                    echo "Build Failed"
                }
            }
        }
         
        stage("Push"){
            steps{
                script{
                    docker.withRegistry('', "${REGISTRY_CRED}") {
                        dockerImg.push()
                    }
                }
            }
            post{
                    success{
                        echo "Push Successful"
                    }
                    failure{
                        echo "Push Failed"
                    }
            }
        }
        
    }
    
    post { 
        always { 
            cleanWs()
        }
    }
}