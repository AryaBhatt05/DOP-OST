pipeline {
  agent any
  tools {
    jdk 'JDK17'
    maven 'M3'
  }
  options {
    timestamps()
    buildDiscarder(logRotator(numToKeepStr: '20'))
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -v'
        sh 'mvn -B -DskipTests=true clean package'
      }
      post {
        success {
          archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
      }
    }
    stage('Test') {
      steps {
        sh 'mvn -B test'
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