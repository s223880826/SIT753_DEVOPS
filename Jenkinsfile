pipeline {
    agent any

    environment {
        CC_TEST_REPORTER_ID = credentials('CODECLIMATE_REPO_TOKEN')
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Abdulqadeer2024/SIT753-6.2HD.git', branch: 'main'
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
            post {
                always {
                    echo 'Build stage completed'
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
