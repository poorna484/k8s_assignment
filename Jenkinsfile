pipeline {
    agent any

    environment {
        // Use the Secret File you uploaded
        KUBECONFIG = credentials('kubeconfig') 
    }

    stages {

        stage('Checkout Code') {
            steps {
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
                sh '''
                echo "Using kubeconfig at $KUBECONFIG"
                kubectl apply -f pod.yaml
                '''
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
