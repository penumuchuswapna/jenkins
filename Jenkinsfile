pipeline {
    agent any

    environment {
        FRONTEND_REPO = 'https://github.com/pveerrotwal/ToDoFastAPI-Frontend.git'
    }

    stages {
        stage('Build Frontend') {
            steps {
                git branch: 'main', url: "${env.FRONTEND_REPO}"
                echo 'Building Frontend'
                bat 'npm install'
                bat 'npm run build'
            }
        }

        stage('Deploy Backend') {
            steps {
                echo 'Deploying Backend'
                bat 'docker-compose -f docker-compose-frontend.yml up -d'
            }
        }

        stage('SonarQube Analysis') {
            when {
                expression {
                    return false // skip for now unless needed
                }
            }
            steps {
                echo 'SonarQube Analysis stage skipped for now'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
            bat 'echo Cleanup or final steps here'
        }
    }
}
