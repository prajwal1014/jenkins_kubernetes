pipeline {
    agent any
    environment {
        GIT_REPO = 'https://github.com/prajwal1014/jenkins_kubernetes.git'
        YAML_FILE = 'ClusterIP.yml'
        K8S_CREDENTIALS = 'k8s-kubeconfig' // Jenkins credential ID for kubeconfig
        KUBECONFIG = '/var/lib/jenkins/.kube/config' // Use Jenkins home directory
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: "${GIT_REPO}"
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                withCredentials([file(credentialsId: "${K8S_CREDENTIALS}", variable: "KUBECONFIG_FILE")]) {
                    sh "mkdir -p /var/lib/jenkins/.kube"
                    sh "cp ${KUBECONFIG_FILE} ${KUBECONFIG}"
                    sh "export KUBECONFIG=${KUBECONFIG} && kubectl apply -f ${YAML_FILE}"
                }
            }
        }
    }
}
