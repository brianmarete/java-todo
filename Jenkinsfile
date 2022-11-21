pipeline {
    agent any

    tools{
        gradle "Gradle-7"
    }


    environment {
        VERSION_NUMBER = '1.0'
    }

    stages {
        stage('Clone repository') {
            steps {
                echo 'Cloning repository'
                 git "https://github.com/nivlapeter/java-todo.git"
            }
        }
        stage('Build ') {
            steps {
                echo "Build number ${BUILD_NUMBER}"
                // withGradle() {
                    sh 'gradle build'
                // }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the project'
                // withGradle() {
                    sh 'gradle test'
                // }
            }
        }
    }
    post {
        success {
            slackSend color: "good", message: "Build #${BUILD_NUMBER} ran successfully"
        }
        
        failure {
            slackSend color: "danger", message: "Build #${BUILD_NUMBER} failed"
        }
    }
}


