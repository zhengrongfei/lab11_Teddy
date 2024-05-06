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
        stage('Generate Javadoc') {
            steps {
                // 生成 Javadoc
                sh '''
                ${MAVEN_HOME}/bin/mvn -f /Users/rongfeizheng/Desktop/Teedy/docs-web-common/pom.xml javadoc:javadoc \
                -Djansi.passthrough=true -Dfile.encoding=UTF-8
                '''
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
