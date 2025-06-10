pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'javac -cp ".:libs/*" src/tests/LoginTest.java'
            }
        }
        stage('Test') {
            steps {
                sh 'java -cp ".:libs/*:src" tests.LoginTest'
            }
        }
    }
}
