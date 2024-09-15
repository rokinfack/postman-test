pipeline {
    agent any
    stages {
        stage('Install html reporter') {
            steps {
                sh '''
                 npm install -g newman-reporter-htmlextra
                '''
            }
        }
    
 
        stage('Run Newman tests') {
            steps {
                sh '''
                 newman run newman_collections.json \
                --reporters cli,json,junit \
                --reporters cli,htmlextra \
                 --reporter-htmlextra-export ./report.html
                '''
            }
        }
    }
    post {
        always {
            //archiveArtifacts artifacts: 'report.json, report.xml'
            archiveArtifacts artifacts: 'newman/report.html', allowEmptyArchive: true

        }
        success {
            echo 'API Tests Passed!'
        }
        failure {
            echo 'API Tests Failed. Check the reports for details.'
        }
    }
}
