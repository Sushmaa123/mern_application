pipeline {
    agent any
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages {
        stage('git checkout') {
            steps {
                git 'https://github.com/Sushmaa123/mern_application'
            }
        }
        stage ('sonar code analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
               sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=mern-app \
               -Dsonar.java.binaries=. \
               -Dsonar.projectKey=mern_application'''
                }
            }
        }
        stage('Docker Compose') {
            steps {
                script{
                    sh 'docker-compose up -d'
                }
            }
        }
        stage('docker push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                       sh 'docker tag frontend sushmaagowdaa/frontend'
                       sh 'docker tag backend sushmaagowdaa/backend'
                       sh 'docker push sushmaagowdaa/frontend'
                       sh 'docker push sushmaagowdaa/backend' 
                    }
                }
            }
        }
    }
}
