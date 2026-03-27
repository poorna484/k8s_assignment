pipeline {
    agent any

    environment {
        // Use the kubeconfig file stored in Jenkins credentials
        KUBECONFIG = credentials('kubeconfig')
    }

    stages {

        stage('Checkout Code') {
            steps {
                // Checkout your GitHub repo
                git branch: 'main', url: 'https://github.com/poorna484/k8s_assignment.git'
            }
        }

        stage('Verify Files') {
            steps {
                // List files in workspace to confirm pod.yaml exists
                sh 'ls -l'
            }
        }

        stage('Deploy Pod') {
            steps {
                // Deploy the pod using kubectl
                sh '''
                echo "Deploying pod using kubeconfig..."
                kubectl apply -f pod.yaml
                echo "Waiting 5 seconds for pod to initialize..."
                sleep 5
                kubectl get pods -o wide
                '''
            }
        }

        stage('Post-Deployment') {
            steps {
                // Optional: describe pod for more info
                sh 'kubectl describe pod my-first-pod || true'
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
