//CD Jenkinsfile for GCBank Application

pipeline {
    agent any
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'Git-creds', url: 'https://github.com/sathish103/Multi-Tier-BankApp-CD.git'
            }       
        }
    
        stage('Kubernetes Deploy') {
            steps {
                script {
                withKubeConfig(caCertificate: '', clusterName: 'project-cluster', contextName: '', credentialsId: 'k8s-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://B50AD206B084BF5E3FD0F94E02C8FD5C.gr7.us-east-1.eks.amazonaws.com') {
                    sh "kubectl apply -f manifest/deployment.yaml"
                    sh "kubectl apply -f manifest/hpa.yaml"
                    sleep 30
                    sh "kubectl apply -f manifest/cluster_issuer.yaml"
                    sh "kubectl apply -f manifest/ingress.yaml"
                    sh "kubectl get pods -n webapps"
                    sh "kubectl get svc -n webapps"
                }
                }
            }
        }
    }
}