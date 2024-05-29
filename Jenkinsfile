pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/s223880826/SIT753_DEVOPS.git', branch: 'main'
            }
        }
 
        stage('Debug') {
            steps {
                script {
                    // List the contents of the workspace to debug paths
                    bat 'dir /S'
                }
            }
        }
 
        stage('Build') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    env.APP_NAME = packageJson.name
                }
                bat 'npm install'
                bat '''
                    curl -L https://github.com/newrelic/newrelic-cli/releases/download/v0.33.1/newrelic-cli_0.33.1_Windows_x86_64.zip -o newrelic-cli.zip
                    tar -xf newrelic-cli.zip
                    set PATH=%PATH%;%cd%\\newrelic-cli
                '''
                echo 'Build stage completed'
            }
        }
 
        stage('Test') {
            steps {
                bat 'npm test'
                echo 'Test stage completed'
            }
        }
    }
}
