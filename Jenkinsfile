node{
  echo 'Welcome jekins from Git'
  stage('SCM GIT checkout'){
    git branch: 'main', url: 'https://github.com/HWHospital2024/HW_Hospital_App'
  }
  stage('Compile Package'){
    sh 'npm i'
  }
  
}
