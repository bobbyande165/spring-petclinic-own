pipeline{
    agent {label 'JAVA2'}
    triggers {
        pollSCM('* * * * *')
    }
    stages{
        stage('git clone'){
            steps{
                git url: 'https://github.com/bobbyande165/spring-petclinic-own.git'
                branch: 'main'
            }
        }
        stage('build and scan'){
             steps {
        withCredentials([string(credentialsId: 'spc_token_id', variable: 'SONAR_TOKEN')]) {
            withSonarQubeEnv('url_of_sonarqube') {
                sh """mvn package sonar:sonar \
                -Dsonar.projectKey=bobbyande165_spring-petclinic-own \
                -Dsonar.organization=bobbyande165 \
                -Dsonar.host.url=https://sonarcloud.io/ \
                -Dsonar.login=$SONAR_TOKEN"""
            }
        }
    }
        }
    }
}