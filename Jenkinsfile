pipeline {
    agent any
    environment {
        IMAGE_NAME = 'cocozheng/teedy' // 替换为你的 Docker Hub 用户名和镜像名称
        REGISTRY_CREDENTIALS_ID = '6f8d5d60-2e21-4f7e-9113-dc51468d058d' // 替换为你的 Jenkins 中配置的 Docker Hub 凭证的 ID
    }
    stages {
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    kubectl('delete -f k8s/deployment.yaml --ignore-not-found=true')
                    kubectl('apply -f k8s/deployment.yaml')
                }
            }
        }
    }

}
