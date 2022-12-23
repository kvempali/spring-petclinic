pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        sh './mvnw spring-javaformat:apply clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.host.url=http://localhost:9000/ \\
  -Dsonar.projectKey=Petclinic \\
  -Dsonar.login=sqp_cdc961205eb429374d9d007f6a9860fc3f7a8491'''
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
      }
    }

    stage('Package') {
      steps {
        sh './mvnw jar:jar package -DskipTests=true'
      }
    }

    stage('Integration Test') {
      steps {
        node(label: 'test') {
          sh './mvnw verify -P tomcat90'
        }

      }
    }

  }
}