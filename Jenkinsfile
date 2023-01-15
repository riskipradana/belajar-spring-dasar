pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                echo 'Stage - Step Test Push From SCM!'
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