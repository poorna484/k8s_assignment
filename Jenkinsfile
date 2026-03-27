pipeline {
    agent { label 'my-node' }

    environment {
        KUBECONFIG = credentials('kubeconfig')
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: '',https://github.com/poorna484/k8s_assignment.git
                    credentialsId: 'git_credentials'
            }
        }

        stage('Verify Files') {
            steps {
                sh 'ls -l'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                export KUBECONFIG=$KUBECONFIG
                kubectl apply -f pod.yaml
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                export KUBECONFIG=$KUBECONFIG
                kubectl get pods
                '''
            }
        }
    }
}
