pipeline {
    agent { label 'my-node' }

    stages {

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/poorna484/k8s_assignment.git',
                    credentialsId: 'git_credentials'
            }
        }

        stage('Verify YAML') {
            steps {
                sh 'cat pod.yaml'
            }
        }

        stage('Deploy Pod') {
            steps {
                sh 'kubectl apply -f pod.yaml'
            }
        }
    }
}
