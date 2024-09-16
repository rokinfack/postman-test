pipeline {
   agent {
        docker { 
            image 'postman/newman'
            args "--entrypoint=''"
        }
    }
    stages {
        stage('Installation de newman') {
            steps {
                sh 'newman --version'
            }
        }

        stage('Run Newman tests') {
            steps {
                sh '''
                 mkdir -p reports
                 newman run newman_collections.json \
                 --reporters cli,json,junit,htmlextra \
                --reporter-json-export ./reports/report.json \
                --reporter-junit-export ./reports/report.xml \
                 --reporter-htmlextra-export ./reports/myreport.html 
                '''
            }
        }
    }
    
    post {
        always {
            // Archiver les rapports générés
            archiveArtifacts artifacts: 'reports/*.html', allowEmptyArchive: true

            // Publier le rapport HTML
            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'reports',
                reportFiles: 'myreport.html',
                reportName: 'My Reports',
                reportTitles: 'The Report'
            ])

            junit "reports/myreport.xml"
        }

        
    }
}
