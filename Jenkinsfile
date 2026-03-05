pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: "${env.BRANCH_NAME}",
                url: 'https://github.com/shaibazkhan1998-collab/java-web-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(
                    credentialsId: 'tomcat',
                    url: 'http://172.28.189.81:8090/',
                    path: '',
                    alternativeDeploymentContext: ''
                )],
                contextPath: 'java-web-app-master',
                war: '**/*.war'
            }
        }
    }
}
