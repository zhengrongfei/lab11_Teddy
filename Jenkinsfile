pipeline {
    agent any



    stages {
          stage('Build'){
            steps{
              sh 'mvn -B -DskipTests clean package'
            }
        }

        stage('pmd') {
            steps {
                // 生成 Javadoc
                sh 'mvn clean -DskipTests install'
            }
        }

          stage('Generate Surefire Reports') {
            steps {
                // 确保测试报告可以生成，即使测试失败
                script {
                    sh 'mvn surefire-report:report'
                }
            }
        }
        

        stage('Generate Javadoc') {
            steps {
                // 生成 Javadoc
                sh 'mvn javadoc:javadoc -Dmaven.javadoc.failOnError=false'
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
