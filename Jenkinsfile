node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    powershell "mvn clean verify sonar:sonar -Dsonar.login=squ_cccbae75dbfb0b153660abf35177a745972a0e1b -Dsonar.projectKey=DeployBack"
  }
}
