node{
    agent {
        label 'Ubuntu-EC2-Instance' // Specify the label of the slave node
    }
    stage('SCM Checkount'){
       git branch: 'main', credentialsId: 'HWhr3000', url: 'https://github.com/HWHospital2024/HW_Hospital_App.git'
    }
    stage ('Compile-package'){
        sh 'npm i'
        sh 'nohup node app.js &' 
    }
}

    
