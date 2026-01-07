pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/louayRm157/Projet-DevOps-ElkachtoulLouay.git'
            }
        }

        stage('Build & Test') {
            steps {
                dir('bonjour-devops') {
                    sh 'mvn -B clean test'
                }
            }
        }

        stage('Package') {
            steps {
                dir('bonjour-devops') {
                    sh 'mvn -B package'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t bonjour-devops:jenkins .'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'bonjour-devops/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline SUCCESS'
        }
        failure {
            echo '❌ Pipeline FAILED'
        }
    }
}
