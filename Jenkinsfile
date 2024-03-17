pipeline {
    agent {
        label 'Ubuntu-EC2-Instance' // Specify the label of the slave node
    }
    stages {
        // Define stages of your pipeline
          stage('SCM GIT checkout'){
              steps {
              git branch: 'main', url: 'https://github.com/HWHospital2024/HW_Hospital_App'
              }
          }
          stage('Compile Package'){
            steps{
                sh 'npm i'
              }
          }
      }
}
