pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/poorna484/k8s_assignment.git'
            }
        }

        stage('Deploy Pod') {
            steps {
                sh '''
                export KUBECONFIG=/var/lib/jenkins/.kube/config
                kubectl apply -f pod.yaml
                '''
            }
        }

        stage('Verify Pod') {
            steps {
                sh '''
                export KUBECONFIG=/var/lib/jenkins/.kube/config
                kubectl get pods
                '''
            }
        }
    }
}
