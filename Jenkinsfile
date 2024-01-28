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
          sh '''mvn sonar:sonar \\
  -Dsonar.projectKey=devopscmu-assignment-petclinic-app \\
  -Dsonar.projectName=\'devopscmu-assignment-petclinic-app\' \\
  -Dsonar.host.url=http://13.201.49.95:9000 \\
  -Dsonar.token=sqp_f72db1e138d794b8c49150429f141063c32d88fd'''
        }

      }
    }

    stage('Run Tests') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Package') {
      steps {
        sh 'mvn package'
      }
    }

  }
  post {
    always {
      junit(testResults: '**/target/surefire-reports/*.xml', allowEmptyResults: true)
    }

  }
}