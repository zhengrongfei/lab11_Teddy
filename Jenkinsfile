pipeline {
    agent any



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
        }
        stage('Generate Javadoc') {
            steps {
                // 生成 Javadoc
                sh 'mvn javadoc:javadoc'
            }
        }

         stage('pmd') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
    }
     post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}
