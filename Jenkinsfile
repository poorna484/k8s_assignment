pipeline {
    agent any

    environment {
        // Kubeconfig credential ID
        KUBECONFIG = credentials('git_credentials')  
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Use Git credentials to clone the repo
                git branch: 'main', url: 'https://github.com/poorna484/k8s_assignment.git', credentialsId: 'git_credentials'
            }
        }

        stage('Deploy Pod') {
            steps {
                // Deploy the pod using the YAML file in repo
                sh 'kubectl apply -f pod.yaml'
            }
        }

        stage('Verify Pod') {
            steps {
                // Check pod status
                sh 'kubectl get pods -o wide'
            }
        }
    }
}
