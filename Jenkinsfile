pipeline {
    agent any

    environment {
        KUBECONFIG = credentials('kubeconfig')  // Jenkins secret file ID
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
                # Apply pod.yaml to the cluster
                kubectl apply -f pod.yaml
                # Verify pod status
                kubectl get pods -o wide
                '''
            }
        }

        stage('Post-Deployment') {
            steps {
                echo "Deployment finished successfully!"
            }
        }
    }
}
