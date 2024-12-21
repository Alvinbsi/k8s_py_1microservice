pipeline {
    agent any

    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Alvinbsi/k8s_py_1microservice.git'
            }
        }
    }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t k8s_dec21img /var/lib/jenkins/workspace/k8s_dec21'
                sh 'sudo docker tag k8s_dec21img alvinselva/k8s_dec21img:latest'
                sh 'sudo docker tag k8s_dec21img alvinselva/k8s_dec21img:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push alvinselva/k8s_dec21img:latest'
                sh 'sudo docker image push alvinselva/k8s_dec21img:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/k8s_dec21/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
}
