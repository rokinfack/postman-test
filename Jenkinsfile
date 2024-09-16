pipeline {
    agent any
    stages {
        stage('Run Newman tests') {
            steps {
                sh '''
                 newman run newman_collections.json \
                --reporters cli,json,junit \
                --reporters cli,htmlextra \
                 --reporter-htmlextra-export ./newman/report.html \
                 --reporter-htmlextra-theme default
                  ls -la ./newman
                '''
            }
        }
    }
   post {
        always {
            archiveArtifacts artifacts: 'newman/*.html', allowEmptyArchive: true
            script {
                // Vérifiez la présence des fichiers HTML
                def files = sh(script: 'ls -la newman/*.html', returnStdout: true).trim()
                if (!files) {
                    error "Aucun fichier HTML trouvé dans le répertoire 'newman'."
                }
            }
            publishHTML(target: [
                reportDir: 'newman',
                reportFiles: '*.html',
                keepAll: true,
                alwaysLinkToLastBuild: true,
                allowMissing: true
            ])
        }
    }
}
