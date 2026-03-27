pipeline {
    agent any

    environment {
        KUBECONFIG = credentials('kubeconfig')
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/poorna484/k8s_assignment.git'
            }
        }

        stage('Deploy Pod to Kubernetes') {
            steps {
                sh '''
                export KUBECONFIG=$KUBECONFIG
                kubectl apply -f pod.yaml
                '''
            }
        }

        stage('Verify Pod') {
            steps {
                sh '''
                export KUBECONFIG=$KUBECONFIG
                kubectl get pods
                '''
            }
        }
    }
}
