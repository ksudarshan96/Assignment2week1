pipeline {
  agent any
  tools { 
    jdk 'jdk-21'      // must match your Tools name
    maven 'maven-3'   // must match your Tools name
  }

  stages {
    stage('Checkout') { steps { checkout scm } }

    stage('Env Check') {
      steps {
        bat 'java -version'
        bat 'mvn -version'
      }
    }

    stage('Build') {
      steps {
        bat 'mvn -B -e clean package'
      }
    }

    stage('Test') {
      steps {
        bat 'mvn -B -e test'
      }
    }

    stage('Archive') {
      steps {
        junit allowEmptyResults: true, testResults: '**/surefire-reports/*.xml'
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }
  }

  post { always { echo 'Build finished. Check artifacts & test reports.' } }
}
