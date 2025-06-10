pipeline {
    agent any

    environment {
        // You can customize these if needed
        MAVEN_OPTS = "-Dmaven.test.failure.ignore=false"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        always {
            echo 'Publishing test results and archiving artifacts...'
            junit 'target/surefire-reports/*.xml'

            archiveArtifacts artifacts: 'target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: 'target/surefire-reports/**/*.*', allowEmptyArchive: true
        }

        failure {
            echo 'Build failed. Check test reports or logs for details.'
        }

        success {
            echo 'Build completed successfully.'
        }
    }
}
