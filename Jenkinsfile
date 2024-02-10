pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.projectKey=petclinic \\
  -Dsonar.projectName=\'petclinic\' \\
  -Dsonar.host.url=http://3.87.83.57:9000 \\
  -Dsonar.token=sqp_e627de67cb90e5c92a64937372d0bc0b2d4023c5'''
      }
    }

    stage('Unit test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
        junit '**/target/surefire-reports/'
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
      }
    }

  }
}