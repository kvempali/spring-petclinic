pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/kvempali/spring-petclinic.git', branch: 'pipeline', changelog: true)
      }
    }

    stage('Maven Build') {
      steps {
        sh 'mvn clean compile'
      }
    }

    stage('Static Analysis') {
      agent any
      steps {
        sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
      }
    }

  }
}