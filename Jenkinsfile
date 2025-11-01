pipeline {
  agent any
  tools {
    jdk 'JDK'
    maven 'Maven'
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        bat 'mvn -v'
        bat 'mvn -B -DskipTests=true clean package'
      }
      post {
        success {
          archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
      }
    }
    stage('Test') {
      steps {
        bat 'mvn -B test'
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
        }
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}
