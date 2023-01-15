pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Stage Build - Step 1!'
            }
        }
        stage('Test') {
            steps {
                echo 'Stage Test - Step 1!'
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