pipeline {
    agent any

    environment {
        KUBECONFIG = '/home/ubuntu/.kube/config' // Path to Minikube kubeconfig
    }

    stages {
        stage('Create Pod') {
            steps {
                sh """
                    echo 'apiVersion: v1
                    kind: Pod
                    metadata:
                      name: my-pod
                      labels:
                        app: my-app
                    spec:
                      containers:
                      - name: my-container
                        image: nginx:latest
                        ports:
                        - containerPort: 80' > pod.yaml

                    kubectl apply -f pod.yaml
                    kubectl get pods -o wide
                """
            }
        }
    }

    post {
        always {
            echo 'Finished pipeline'
        }
    }
}
