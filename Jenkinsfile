pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('Build') {
            steps {
                sh 'pwd'
                sh 'ls -la'
                echo 'Webhook Triggered Successfully'
            }
        }
    }
}
