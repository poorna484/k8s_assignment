pipeline {
    agent any

    environment {
        KUBECONFIG_CREDENTIAL = 'kubeconfig'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/poorna484/k8s_assignment.git'
            }
        }

        stage('Deploy Pod') {
            steps {
                withCredentials([file(credentialsId: "${KUBECONFIG_CREDENTIAL}", variable: 'KUBECONFIG')]) {
                    
                    sh '''
                    export KUBECONFIG=$KUBECONFIG
                    kubectl apply -f pod.yaml
                    '''
                }
            }
        }

        stage('Verify Pod') {
            steps {
                withCredentials([file(credentialsId: "${KUBECONFIG_CREDENTIAL}", variable: 'KUBECONFIG')]) {
                    
                    sh '''
                    export KUBECONFIG=$KUBECONFIG
                    kubectl get pods
                    '''
                }
            }
        }
    }
}
