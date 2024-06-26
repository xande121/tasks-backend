pipeline {
  agent any
  stages {
    stage ('Build Backend') {
      steps {
        bat 'mvn clean package -DskipTests=true'
      }
    }
    stage ('Unit Tests') {
      steps {
        bat 'mvn test'
      }
    }
    stage ('Sonar Analysis') {
        environment {
            scannerHome = tool 'SONAR_SCANNER'
        }
      steps {
        withSonarQubeEnv('SONAR_LOCAL'){

        bat "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.login=5e0e2888a29b3f01cc9e76e9f2ad3a114c70f1a7 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java"
      
        }
      }
    }
    stage ('Quality Gate'){
      steps {
        sleep(5)
      }
    }
    stage ('Deploy Backend'){
      steps{
        deploy adapters: [tomcat8(credentialsId: 'TomcatLogin', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'
      }
    }
    stage ('API Test'){
      steps{
        dir('api-test'){
          git credentialsId: 'LoginGit', url: 'https://github.com/xande121/tasks-api-test'
          bat 'mvn test'
        }
      }
    }
    stage ('Deploy Frontend'){
      steps{
        dir('frontend'){
          git credentialsId: 'LoginGit', url: 'https://github.com/xande121/tasks-frontend'
          bat 'mvn clean package'
          deploy adapters: [tomcat8(credentialsId: 'TomcatLogin', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks', war: 'target/tasks.war'
        }
      }
    }
  }
}