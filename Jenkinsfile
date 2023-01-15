pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat("mvn clean install -DskipTests")
                echo 'Stage Build - Step 1!'
                script {
                    echo 'script'
                }
            }
        }
        stage('Test') {
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