pipeline {
    agent any
 
    environment {
        CC_TEST_REPORTER_ID = credentials('CODECLIMATE_REPO_TOKEN')
    }
 
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
            }
            
        }
 
        stage('Test') {
            steps {
                bat 'npm test'
            }
            
        }
 
        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying the application...'
                    // Add your deployment script/commands here
                }
            }
            
        }
 
        stage('Release') {
            steps {
                script {
                    echo 'Releasing the application to production...'
                    withCredentials([string(credentialsId: 'NEW_RELIC_API_KEY', variable: 'NEW_RELIC_API_KEY')]) {
                        // Use the New Relic deployment command
                        bat 'newrelic-admin deployment --appname YourAppName --description "Deployment via Jenkins" --apikey %NEW_RELIC_API_KEY%'
                    }
                }
            }
            
        }
 
        stage('Monitor and Alert') {
            steps {
                script {
                    echo 'Verifying monitoring setup in New Relic...'
                    // Here, you might include steps to check the status of the New Relic agent, ensure it's reporting data, etc.
                    // This is a placeholder, actual commands depend on your operational setup.
                }
            }
         }   
    }
 
    post {
        always {
            cleanWs()
        }
    }
}
