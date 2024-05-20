pipeline {
    agent any
    environment {
        IMAGE_NAME = 'cocozheng/teedy' // 替换为你的 Docker Hub 用户名和镜像名称
        REGISTRY_CREDENTIALS_ID = '6f8d5d60-2e21-4f7e-9113-dc51468d058d' // 替换为你的 Jenkins 中配置的 Docker Hub 凭证的 ID
    }
    stages {
        stage('Build Image') {
            steps {
                script {
                    // 构建 Docker 镜像并标记
                    docker.build(IMAGE_NAME)
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    // 登录到 Docker Hub 并推送镜像
                    docker.withRegistry('https://registry.hub.docker.com', REGISTRY_CREDENTIALS_ID) {
                        docker.image(IMAGE_NAME).push('latest')
                    }
                }
            }
        }
        stage('Deploy Containers') {
            steps {
                script {
                    // 运行三个 Docker 容器实例，每个实例映射到不同的端口
                    docker.image(IMAGE_NAME).run("-d -p 8082:8080 --name teedy_manual02")
                    docker.image(IMAGE_NAME).run("-d -p 8083:8080 --name teedy_manual03")
                    docker.image(IMAGE_NAME).run("-d -p 8084:8080 --name teedy_manual01")
                }
            }
        }
    }
}
