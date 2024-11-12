pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Package') {
            steps {
                sh './gradlew compileJava'
            }
        }
        stage('Docker build') {
            steps {
                sh "docker build -t calculatrice ."
            }
        }
        stage('Docker push') {
            steps {
                sh "docker images"
            }
        }
        stage('Déploiement sur staging') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Déploiement en cours...'
                // Ajoutez ici les commandes pour le déploiement en staging
            }
        }
        stage('Test d\'acceptation') {
            steps {
            sleep 60
            sh "chmod +x acceptance_test.sh && ./acceptance_test.sh"
            }
        }
    }
    post {
        always {
            script {
                try {
                    sh "docker rm calculatrice"
                } catch (Exception e) {
                    echo "Aucun conteneur Docker à arrêter"
                }
            }
        }
    }
}


