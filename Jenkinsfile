pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/<your-username>/<repo-name>.git'
            }
        }

        stage('Verify YAML') {
            steps {
                sh 'echo "Checking pod.yaml file..."'
                sh 'cat pod.yaml'
            }
        }

        stage('Deploy Pod') {
            steps {
                sh '''
                echo "Deploying pod to Kubernetes..."
                kubectl apply -f pod.yaml
                '''
            }
        }

        stage('Verify Pod') {
            steps {
                sh '''
                echo "Checking pod status..."
                kubectl get pods -o wide
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Pod deployed successfully!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
