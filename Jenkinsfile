pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Iam-mithran/k8repo.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'docker build -t newimage /var/lib/jenkins/workspace/k8'
                sh 'docker tag newimage iammithran/newimage:latest'
                sh 'docker tag newimage iammithran/newimage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'docker image push --all-tags iammithran/newimage'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'kubectl apply -f /var/lib/jenkins/workspace/k8/pod.yaml'
                sh 'kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
