pipeline {
    agent any

    environment {
        KUBECONFIG = '/var/lib/jenkins/.kube/config'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/poorna484/k8s_assignment.git'
            }
        }

        stage('Verify Pod File') {
            steps {
                sh 'ls -l pod.yaml'
            }
        }

        stage('Apply Pod') {
            steps {
                sh 'kubectl apply -f pod.yaml'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed!'
        }
    }
}
