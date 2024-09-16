pipeline {
    agent any
    stages {
        stage('Run Newman tests') {
            steps {
                sh '''
                 mkdir -p reports
                 newman run newman_collections.json \
                --reporters cli,json,junit \
                -r cli,htmlextra \
                 --reporter-htmlextra-export ./reports/myreport.html \
                 --reporter-htmlextra-theme default
                  ls -la ./reports
                  cat ./reports/myreport.html
                '''
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'reports/*.html', allowEmptyArchive: true
            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'reports',
                reportFiles: 'myreport.html',
                reportName: 'My Reports',
                reportTitles: 'The Report'
            ])
        }
    }
}
