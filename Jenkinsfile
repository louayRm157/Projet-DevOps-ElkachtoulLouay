pipeline {
    agent any

    tools {
        maven 'Maven'   // doit correspondre au nom dans Jenkins (Global Tool)
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
                    bat 'mvn clean test'
                }
            }
        }

        stage('Package') {
            steps {
                dir('bonjour-devops') {
                    bat 'mvn package'
                }
            }
        }

        stage('Docker Build') {
            steps {
                // Dockerfile est à la racine, donc contexte = "."
                bat 'docker build -t bonjour-devops:jenkins .'
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
