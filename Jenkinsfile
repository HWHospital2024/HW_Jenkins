node{
    agent {
        label 'Ubuntu-EC2-Instance' // Specify the label of the slave node
    }
    stage('SCM Checkount'){
        git branch: 'main', url: 'https://github.com/HWHospital2024/HW_Hospital_App'
    }
    stage ('Compile-package'){
        sh 'npm i'
    }
}

    
