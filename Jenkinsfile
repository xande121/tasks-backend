node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    sh "mvn clean verify sonar:sonar -Dsonar.projectKey=DeployBack"
    /*def mvn = tool 'Default Maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=DeployBack"
    }*/
  }
}
