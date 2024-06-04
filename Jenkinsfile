node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    powershell "mvn clean verify sonar:sonar -Dsonar.projectKey=DeployBack"
  }
}
