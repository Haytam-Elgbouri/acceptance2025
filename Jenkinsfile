pipeline {
    agent any
    stages {
        
        stage('Package') {
            steps {
                sh './gradlew build'
            }
        }
        stage('Docker build') {
            steps {
                sh "docker build -t localhost:5000/calculatric ."
            }
        }
        stage('Docker push') {
            steps {
                sh "docker push localhost:5000/calculatric"
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
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Tests d\'acceptation en cours...'
                // Ajoutez ici les tests d'acceptation
            }
        }
    }
}


