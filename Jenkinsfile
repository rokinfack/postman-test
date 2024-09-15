pipeline {
    agent any
    stages {
        stage('Run Newman tests') {
            steps {
                sh '''
                newman run newman_collections.json \
                --reporters cli,json,junit \
                --reporter-json-export $WORKSPACE/report.json \
                --reporter-junit-export $WORKSPACE/report.xml
                '''
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'report.json, report.xml'
        }
        success {
            echo 'API Tests Passed!'
        }
        failure {
            echo 'API Tests Failed. Check the reports for details.'
        }
    }
}
