pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('pmd') {
            steps {
                bat 'mvn clean install -DskipTests'
                bat 'mvn pmd:pmd'
            }
        }
        stage('Doc') {
            steps {
                bat 'mvn javadoc:jar'
            }
        }
        stage('Test Report') {
            steps {
                bat 'mvn test'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true

            archiveArtifacts artifacts: '**/target/custom-surefire-reports/**', fingerprint: true
        }
    }
}
