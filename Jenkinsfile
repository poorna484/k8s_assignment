pipeline {
    agent any

    environment {
        // Inject the kubeconfig file stored in Jenkins credentials
        KUBECONFIG = credentials('kubeconfig')
    }

    stages {

        stage('Checkout Code') {
            steps {
                // Checkout your repository (optional if pod.yaml is already in workspace)
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
        success {
            echo 'Pod applied successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
