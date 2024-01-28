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
      agent any
      steps {
        sh 'mvn sonar:sonar -Dsonar.projectKey=devopscmu-assignment-petclinic-app -Dsonar.projectName=\'devopscmu-assignment-petclinic-app\' -Dsonar.host.url=http://13.201.49.95:9000 -Dsonar.token=sqp_f72db1e138d794b8c49150429f141063c32d88fd'
      }
    }

  }
}