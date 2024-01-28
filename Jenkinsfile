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
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-api'){
                        sh 'mvn clean package sonar:sonar'

                    }
                }
            }
        }
        stage('Quality Gate Status'){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'

                    
                }
            }
        }
        stage('Uploading war file to Nexus'){
            steps{
                script{
                    def readPomVersion = readMavenPom file: 'pom.xml'
                    nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: 'nexus-auth', groupId: 'com.example', nexusUrl: '35.154.184.21:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'demo-release', version: "${readPomVersion.version}"

                    
                }
            }
        }
    }
}
    

    

