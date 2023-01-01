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
    stage('Test the App') {
      steps {
        sh 'gradle test'
      }
    }
    stage('Deploy to Heroku') {
      steps {
        withCredentials([usernameColonPassword(credentialsId: 'af7ffbc3-0cc5-4ff7-a50d-b0e970c8ffe3', variable: 'HEROKU_CREDENTIALS')]) {
          sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/glacial-beyond-51734.git'
        }
      }
    }
  }
  post {
        success {
      slackSend message: 'Successful'
        }
        failure {
      slackSend message: 'Failed'
        }
  }
}
