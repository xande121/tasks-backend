node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    powershell "mvn clean verify sonar:sonar -Dsonar.login=admin -Dsonar.password=99684 -Dsonar.projectKey=DeployBack"
  }
}
