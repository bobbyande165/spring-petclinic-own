pipeline{
    agent {label 'JAVA1'}
    triggers {
        pollSCM('* * * * *')
    }
    stages{
        stage('git clone'){
            steps{
                git(
                    branch: 'main',
                    url: 'https://github.com/bobbyande165/spring-petclinic-own.git'
                )
            }
        }
        stage('build and scan'){
             steps {
        withCredentials([string(credentialsId: 'SONAR', variable: 'SONAR_TOKEN')]) {
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