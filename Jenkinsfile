pipeline {
    agent any
    stages {
        stage('Install dependencies') {
            steps {
                // Installer Newman si ce n'est pas déjà fait
                sh 'newman --version'
            }
        }
        stage('Run Newman tests') {
            steps {
                // Exécuter les tests API avec une collection Postman locale
                sh '''
                newman run newman_collections.json
                '''
            }
        }
    }
  
}
