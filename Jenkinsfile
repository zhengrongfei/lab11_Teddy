pipeline {
    agent any

    tools {
        // 确保 Jenkins 使用 Maven 工具
        // 'Maven_3_6_3' 是 Maven 工具的名称，你需要在 Jenkins 配置中设置它
        maven 'Maven_3_6_3'
    }

    stages {
          stage('Build'){
            steps{
              sh 'mvn -B -DskipTests clean package'
            }
        }
      
        stage('Generate Surefire Reports') {
            steps {
                // 确保测试报告可以生成，即使测试失败
                script {
                    try {
                        sh 'mvn surefire-report:report'
                    } catch (Exception e) {
                        echo "Tests failed, but Surefire reports are being generated."
                    }
                }
            }
            post {
                always {
                    // 存档 surefire 报告
                    archiveArtifacts artifacts: 'target/surefire-reports/*.xml', allowEmptyArchive: true
                }
            }
        }
        stage('Generate Javadoc') {
            steps {
                // 生成 Javadoc
                sh 'mvn javadoc:javadoc'
            }
            post {
                always {
                    // 存档生成的 Javadoc
                    archiveArtifacts artifacts: 'target/site/apidocs/**/*', allowEmptyArchive: true
                }
            }
        }
    }
    post {
        // 在整个流水线结束后运行
        always {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
        // 如果构建失败，发送通知
        failure {
            echo '构建失败！'
        }
    }
}
