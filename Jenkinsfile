pipeline {
    agent any

    environment {
        K8S_TOKEN  = credentials('k8s-token')  // The Jenkins Secret Text ID
        K8S_SERVER = 'https://127.0.0.1:6443' // Replace with your Kubernetes API server
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/poorna484/k8s_assignment.git'
            }
        }

        stage('Verify Files') {
            steps {
                sh 'ls -l'
            }
        }

        stage('Configure kubectl') {
            steps {
                sh '''
                # Configure temporary kubeconfig
                kubectl config set-cluster jenkins-cluster --server=$K8S_SERVER --insecure-skip-tls-verify=true
                kubectl config set-credentials jenkins-user --token=$K8S_TOKEN
                kubectl config set-context jenkins-context --cluster=jenkins-cluster --user=jenkins-user
                kubectl config use-context jenkins-context
                '''
            }
        }

        stage('Deploy Pod') {
            steps {
                sh '''
                echo "Deploying pod..."
                kubectl apply -f pod.yaml
                kubectl get pods -o wide
                '''
            }
        }

        stage('Post-Deployment') {
            steps {
                echo "Deployment completed successfully!"
            }
        }
    }

    post {
        failure {
            echo "Pipeline failed. Check logs for errors."
        }
        success {
            echo "Pipeline finished successfully."
        }
    }
}
