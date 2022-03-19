pipeline{
    agent any
    stages {
        stage('Build Maven') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'devopshint', url: 'https://github.com/devopshint/jenkins...]]])

             
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t devopshint/nodejsapp-1.0:latest .'
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                script {
                 withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u devopshint -p ${dockerhubpwd}'
                 }  
                 sh 'docker push devopshint/nodejsapp-1.0:latest'
                }
            }
        }
