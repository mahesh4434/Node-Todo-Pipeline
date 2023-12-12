pipeline {
    agent any

    stages {
        stage("Checkout") {
            steps {
                git url: 'https://github.com/mahesh4434/Node-Todo-Pipeline.git', branch: 'main'
            }
        }
        stage("Build & Test"){
            steps{
               script {
                    bat 'docker build -t mahesh4434/node-app .'
                }
            }
        }
        stage("Push on Dockerhub"){
            steps{
            script{
               withCredentials([string(credentialsId: 'Doc-connect', variable: 'DockerSecret')]) {
                env.DOCKER_USERNAME = 'mahesh4434'
                env.DOCKER_PASSWORD = "Dada@7744"
                bat 'docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%'
                bat 'docker push mahesh4434/node-app'
               }
            }
            }
        }
        stage("Kubernetes"){
            steps{
               script{
               kubernetesDeploy (configs: 'deployment.yaml',kubeconfigId: 'k8sconnect')
            }
            }
        }
    }
}
