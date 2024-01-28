pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/kvempali/spring-petclinic.git', branch: 'pipeline', changelog: true)
      }
    }

    stage('Maven Compile') {
      steps {
        sh 'mvn clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        withSonarQubeEnv(installationName: 'devops-cmu-sonar', credentialsId: 'devops-cmu-pipeline-sonar-secret') {
          sh 'mvn sonar:sonar'
        }

      }
    }

  }
}