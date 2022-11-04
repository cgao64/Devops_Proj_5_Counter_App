pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/cgao64/Devops_Proj_5_Counter_App.git'
            }
        }

        stage('UNIT Testing') {
            steps {
                sh 'mvm test'
            }
        }
    }
}