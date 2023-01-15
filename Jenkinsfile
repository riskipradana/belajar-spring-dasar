pipeline {
    agent none

    environment {
        AUTHOR = "Eko Kurniawan Khannedy"
        EMAIL = "echo.khannedy@gmail.com"
        WEB = "https://www.programmerzamannow.com"
    }

    stages {

        stage("Prepare") {
            environment {
                APP = credentials("riski_rahasia")
            }
            agent any
            steps {
                echo("Author ${AUTHOR}")
                echo("Email ${EMAIL}")
                echo("Web ${WEB}")
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
                echo("App User : ${APP_USR}")
                echo("App User : ${APP_PSW}") //string interpolation
                sh('echo "App Password : $APP_PSW" > "rahasia.txt"')
            }
        }

        stage('Build') {
            agent any
            steps {
                bat("mvn clean install -DskipTests")
                echo 'Stage Build - Step 1!'
                script {
                    echo 'script'
                }
            }
        }
        stage('Test') {
            agent any
            steps {
                bat("mvn test")
                echo 'Stage Test - Step 1!'
                script {
                    def data = [
                            "firstName": "Riski",
                            "lastName" : "Pradana"
                    ]
                    writeJSON(file: "data.json", json: data)
                }
            }
        }
        stage('Deploy') {
            agent any
            steps {
                echo 'Stage Deploy - Step 1!'
            }
        }
    }
    post{
        always {
            echo "Post, always!"
        }
        success {
            echo "Post, success!"
        }
        failure {
            echo "Post, failure!"
        }
        cleanup {
            echo "Post, cleanup!"
        }
    }
}