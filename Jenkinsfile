pipeline {
    agent any

    environment {
        KUBECONFIG = credentials('kubeconfig')  // Use your kubeconfig secret
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

        stage('Deploy Pod') {
            steps {
                sh '''
                # Use kubeconfig to deploy pod
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
}
