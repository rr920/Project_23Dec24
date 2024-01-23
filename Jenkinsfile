pipeline {
    agent any
    stages{

        stage('Git Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/rr920/Project_23Dec24.git'
            }
        }
        stage('Unit Testing'){
            steps{
                sh 'mvn test'
            }
        }
        stage('Integration Testing'){
            steps{
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage('Maven Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Static Code Analysis'){
            steps{
                withSonarQubeEnv(credentialsId: 'sonar-api'){
                    sh 'mvn clean package sonar:sonar'

                }
            }
        }
    }
}