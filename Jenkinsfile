pipeline {
    agent any

    environment {
        // Replace 'kubeconfig-secret' with the ID of your Jenkins secret file containing kubeconfig
        KUBECONFIG = credentials('kubeconfig')
    }

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

        stage('Deploy Pod to Kubernetes') {
            steps {
                echo 'Applying pod.yaml to Kubernetes cluster...'
                sh 'kubectl apply -f pod.yaml'
            }
        }

        stage('Verify Pod Deployment') {
            steps {
                echo 'Getting pod status...'
                sh 'kubectl get pods -o wide'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
