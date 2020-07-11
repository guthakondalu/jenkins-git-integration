node {
  stage('SCM') {
    git 'https://github.com/guthakondalu/jenkins-git-integration.git'
  }
  stage('SonarQube analysis') {
    withSonarQubeEnv('My SonarQube Server') {
      sh 'mvn clean package sonar:sonar'
    } // submitted SonarQube taskId is automatically attached to the pipeline context
  }

 stage('Build') {
         sh 'mvn clean package sonar:sonar'
   
  }

   stage('Unit Tests') {
   
      sh 'mvn clean package sonar:sonar'
    
  }

   stage('Deploy') {
    
      sh 'mvn test'
    
  }

   stage('Regression') {
    
      echo 'Regression'
    
  }


}
  
// No need to occupy a node
stage("Quality Gate"){
  timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
    def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
    if (qg.status != 'OK') {
      error "Pipeline aborted due to quality gate failure: ${qg.status}"
    }
  }
}