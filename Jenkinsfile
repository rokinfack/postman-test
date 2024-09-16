pipeline {
    agent any
    stages {
        stage('Run Newman tests') {
            steps {
                sh '''
                 newman run newman_collections.json \
                --reporters cli,json,junit \
                --reporters cli,htmlextra \
                 --reporter-htmlextra-export ./report.html \
                 --reporter-htmlextra-theme default
                  ls -la ./newman
                '''
            }
        }
    }
   post {
        always {
            archiveArtifacts artifacts: 'report.html', allowEmptyArchive: true
            publishHTML(target: [
                reportDir: './',
                reportFiles: 'report.html',
                keepAll: true,
                alwaysLinkToLastBuild: true,
                allowMissing: true
            ])
        }
    }
}
