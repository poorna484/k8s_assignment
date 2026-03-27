pipeline {
    agent any

    environment {
        KUBECONFIG = credentials('kubeconfig') // Jenkins credential ID for your kubeconfig
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/poorna484/k8s_assignment.git'
            }
        }

        stage('Deploy Pod') {
            steps {
                // Apply the pod YAML from the repo
                sh 'kubectl apply -f pod.yaml'
            }
        }

        stage('Verify Pod') {
            steps {
                // Check if the pod is running
                sh 'kubectl get pods -o wide'
            }
        }
    }
}
