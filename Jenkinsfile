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
        stage('Deploy to Heroku') {
            steps {
                withCredentials([usernameColonPassword(credentialsId: 'heroku', variable: 'PASSWORD' )]){
                sh "git push https://${PASSWORD.replace('@','\\@')}@git.heroku.com/cryptic-lowlands-99184.git master"
                // sh 'git push https://nivlapeter:#Royalty@1993@git.heroku.com/mighty-earth-27385.git master'
                // withCredentials([usernameColonPassword(credentialsId: 'heroku', variable: 'HEROKU_CREDENTIALS' )]){
                // sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/cryptic-lowlands-99184.git master'              
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


