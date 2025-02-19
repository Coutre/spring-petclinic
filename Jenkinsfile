pipeline {
    agent any
    
    triggers {
        cron('H/10 * * * 1')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    sh './mvnw clean package'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh './mvnw test'
                }
            }
        }

        stage('Code Coverage') {
            steps {
                script {
                    sh './mvnw jacoco:report'
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'SUCCESS'
        }
        failure {
            echo 'FAIL'
        }
    }
}
