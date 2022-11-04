pipeline {
    agent any

    stages{
        stage('Git Checkout'){
            steps {
                git branch: 'main', url: 'https://github.com/cgao64/Devops_Proj_5_Counter_App.git'
            }
        }

        stage('UNIT Testing'){
            steps {
                sh 'mvm test'
            }
        }

        stage('Integration testing'){
            steps{
                sh 'mvm verify -DiskUnitTests'
            }
        }

        stage("Maven Build"){
            steps {
                sh 'mvn clean install'
            }
        }
        
        stage("Static code analysis"){
            steps{
                script{
                    withSonarQubeEnv(credentialsID: 'sonar-api') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }

        stage('Quality Gate status'){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'

                }
            }
        }

        stage('upload war file to nexus'){
            steps{
                script{

                    def readPomVersion = readMavenPom file: 'pom.xml'
                    nexusArtifactUploader artifacts:
                    [
                        [
                            artifactId: 'springboot',
                            classifier: '', file: 'target/Uber.jar',
                            type: 'jar'
                        ]
                    ]

                    credentialsId: 'nexus-auth',
                    groupId: 'com.example',
                    nexusUrl: '3.225.233.15:8081',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: 'demoapp-replase',
                    version: '1.0.0'
                    version: "${readPomVersion.version}"
                }
            }
        }
    }
}