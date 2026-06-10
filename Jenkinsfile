pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy DEV') {
            when {
                branch 'dev'
            }
            steps {
                sh '''
                echo "Déploiement vers DEV"
                cp -r app/* /opt/web-hosting/dev/app/
                cd /opt/web-hosting/dev
                docker compose restart
                '''
            }
        }

        stage('Deploy TEST') {
            when {
                branch 'test'
            }
            steps {
                sh '''
                echo "Déploiement vers TEST"
                cp -r app/* /opt/web-hosting/test/app/
                cd /opt/web-hosting/test
                docker compose restart
                '''
            }
        }

        stage('Validation avant PROD') {
            when {
                branch 'main'
            }
            steps {
                input message: 'Valider le déploiement en production ?'
            }
        }

        stage('Deploy PROD') {
            when {
                branch 'main'
            }
            steps {
                sh '''
                echo "Déploiement vers PROD"
                cp -r app/* /opt/web-hosting/prod/app/
                cd /opt/web-hosting/prod
                docker compose restart
                '''
            }
        }
    }
}
