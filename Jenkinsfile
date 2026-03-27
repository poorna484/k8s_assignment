pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out repository...'
                git branch: 'main', url: 'https://github.com/poorna484/k8s_assignment.git', credentialsId: 'git_credentials'
            }
        }

        stage('Verify Pod File') {
            steps {
                echo 'Listing pod.yaml...'
                sh 'ls -l pod.yaml'
            }
        }

        stage('Apply Pod to Kubernetes') {
            steps {
                echo 'Applying pod.yaml using minikube kubectl...'
                // Using minikube's kubectl wrapper to avoid kubeconfig/auth issues
                sh 'minikube kubectl -- apply -f pod.yaml'
            }
        }

        stage('Verify Pod') {
            steps {
                echo 'Getting pod status...'
                sh 'minikube kubectl -- get pods -o wide'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
