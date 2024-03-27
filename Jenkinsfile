pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/HWHospital2024/HW_Hospital_App'
            }
        }
        
        stage('Remove Container') {
            steps {
                // Execute the shell script to remove the container
                script {
                    sh '''
                        #!/bin/bash

                        # Get the container ID of the container you want to remove
                        CONTAINER_ID=$(docker ps -aqf "ancestor=hw_hospital_api")

                        # Check if the container ID is not empty
                        if [ -n "$CONTAINER_ID" ]; then
                            # Remove the container
                            docker rm -f "$CONTAINER_ID"
                            echo "Container with ID $CONTAINER_ID removed successfully."
                        else
                            echo "No container found with the specified image."
                        fi
                    '''
                }
            }
        }
        
        stage('Remove Docker Images') {
            steps {
                script {
                    // Define the repository and tag of the image you want to remove
                    def repository = 'hw_hospital_api'
                    def tag = 'latest'

                    // Get the image ID of the specified repository and tag
                    def imageId = sh(script: "docker images -q ${repository}:${tag}", returnStdout: true).trim()

                    // Check if the image ID is not empty
                    if (imageId) {
                        // Remove the image
                        sh "docker rmi ${imageId}"
                        echo "Image ${repository}:${tag} with ID ${imageId} removed successfully."
                    } else {
                        echo "No image found with repository ${repository} and tag ${tag}."
                    }
                }
            }
        }
        
        stage('Run Tests') {
            steps {
                // Install npm dependencies
                sh 'npm i'
                sh 'npm i chai@4'

                // Run Mocha Chai tests
                sh 'npm run test'
            }
        }
        
        stage('Docker build') {   
            steps {
                sh 'docker build -t hw_hospital_api .'
                sh 'nohup docker run -p 3000:3000 hw_hospital_api &'
            }
        }
    }
    post {
        failure {
            mail to: 'hwhr3000@gmail.com',
                 subject: "Pipeline failed: ${currentBuild.fullDisplayName}",
                 body: "The pipeline ${currentBuild.fullDisplayName} has failed. Please check Jenkins for more details."
        }
    }
    
}
