pipeline {
    agent any
    tools{
        maven 'mavin'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/olufuwatobi/publicis-devops']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t olufuwatobi/publicis-devops .'
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