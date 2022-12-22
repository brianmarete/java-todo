pipeline {
  agent any
  tools {
    gradle 'Gradle-7'
  }
  stages {
    stage('clone repository') {
      steps {
        git 'https://github.com/nivlapeter/java-todo.git'
      }
    }
    stage('Build Project') {
      steps {
        sh 'gradle build'
      }
    }
    stage('Test') {
      steps {
        sh 'gradle test'
      }
    }
  }
  post {
    always {
      echo 'Pipeline Finished'
    }
  }
}
