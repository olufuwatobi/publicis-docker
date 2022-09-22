pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/olufuwatobi/publicis-docker']]])
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t olufuwatobi/publicis-docker .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u olutobi -p ${dockerhubpwd}'

}
                   sh 'docker push olutobi/publicis-docker'
                }
            }
        }
        
    }
}