pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/s223880826/SIT753_DEVOPS.git', branch: 'main'
            }
        }
 
        stage('Build') {
            steps {
                echo 'Hello, Jenkins!'
            }
        }
    }
}
