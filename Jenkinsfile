pipeline {
    agent none

    environment {
        AUTHOR = "Eko Kurniawan Khannedy"
        EMAIL = "echo.khannedy@gmail.com"
        WEB = "https://www.programmerzamannow.com"
    }

//  triggers {
//    cron("*/5 * * * *")
//  }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
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
                bat('echo "App Password : $APP_PSW" > "rahasia.txt"')
            }
        }

        stage("Parameter") {
            agent any
            steps {
                echo "Hello ${params.NAME}"
                echo "You description is ${params.DESCRIPTION}"
                echo "Your social medis is ${params.SOCIAL_MEDIA}"
                echo "Need to deploy : ${params.DEPLOY} to deploy!"
                echo "Your secret is ${params.SECRET}"
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
            input {
                message "Can we deploy?"
                ok "Yes, of course"
                submitter "pzn,eko"
                parameters {
                    choice(name: "TARGET_ENV", choices: ['DEV', 'QA', 'PROD'], description: "Which Environment?")
                }
            }
            agent any
            steps {
                echo("Deploy to ${TARGET_ENV}")
            }
        }

        stage("Release") {
            when {
                expression {
                    return params.DEPLOY
                }
            }
            agent any
            steps {
                echo("Release it")
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