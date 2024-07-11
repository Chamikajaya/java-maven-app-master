pipeline {
    agent any  

    tools {
        maven 'maven-v-3.9.8'  // so that mvn command is available in the pipeline
    
    }


    stages {

        stage("build jar artifact") {
            steps {
                echo "Building the jar artifact"
                sh "mvn clean package"
            }
        }

        stage("build Docker image") {
            steps {
                echo "Building Docker image"
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub',
                    passwordVariable: 'DOCKER_HUB_PASSWORD',
                    usernameVariable: 'DOCKER_HUB_USERNAME'
                )]) {
                    sh "docker build -t  chamikajay/demo-app:latest ."  // TODO: dockerfile
                    sh "echo $DOCKER_HUB_PASSWORD | docker login -u $DOCKER_HUB_USERNAME --password-stdin"
                    sh "docker push chamikajay/demo-app:latest"
                }
            }
        }
        
        stage("deploy") {
            steps {
                echo "Deploying the project"
            }
        }
    }

  
}