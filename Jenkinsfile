pipeline {
  agent any
  stages {
    stage('SCM Checkout') {
      steps {
        git(url: 'https://github.com/kvempali/spring-petclinic.git', branch: 'pipeline', changelog: true)
      }
    }

    stage('Compile') {
      steps {
        sh 'mvn clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''mvn sonar:sonar \\
  -Dsonar.projectKey=devopscmu-assignment-petclinic-app \\
  -Dsonar.projectName=\'devopscmu-assignment-petclinic-app\' \\
  -Dsonar.host.url=http://65.0.72.229:9000 \\
  -Dsonar.token=sqp_f72db1e138d794b8c49150429f141063c32d88fd'''
      }
    }

    stage('Unit Tests') {
      steps {
        sh 'mvn test'
        junit(testResults: '**/target/surefire-reports/*.xml', allowEmptyResults: true)
      }
    }

    stage('Package') {
      steps {
        sh 'mvn package'
      }
    }

  }
}