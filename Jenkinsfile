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
        stage('Build Project') {
            steps {
                echo "Build number ${BUILD_NUMBER}"
                // withGradle() {
                    sh 'gradle build'
                // }
            }
        }
        stage('Test Project') {
            steps {
                echo 'Testing the project'
                // withGradle() {
                    sh 'gradle test'
                // }
            }
        }
        stage('Deploy to Heroku') {
            steps {
                withCredentials([usernameColonPassword(credentialsId: 'heroku', variable: 'HEROKU_CREDENTIALS' )]){
                sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/cryptic-lowlands-99184.git'              
            }
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



