pipeline {
    agent any

    environment {
        KUBECONFIG = credentials('kubeconfig') // Jenkins credential ID for your kubeconfig
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout your repository containing pod.yaml
                git branch: 'main', url: 'https://github.com/poorna484/k8s_assignment.git'
            }
        }

        stage('Create Pod') {
            steps {
                // Apply the pod manifest
                sh 'kubectl apply -f pod.yaml'
            }
        }

        stage('Verify Pod') {
            steps {
                // Check if pod is running
                sh 'kubectl get pods -o wide'
            }
        }
    }

    post {
        success {
            echo 'Pod created successfully!'
        }
        failure {
            echo 'Something went wrong while creating the pod.'
        }
    }
}
