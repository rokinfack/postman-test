pipeline {
     agent {
        docker {
            image 'postman/newman'  // Using the official Newman Docker image
            args '-v $WORKSPACE:/newman'  // Mount Jenkins workspace to a writable directory
        }
    }
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
                newman run newman_collections.json \
                 --reporters cli,json,junit \
                --reporter-json-export /etc/newman/report.json \
                --reporter-junit-export /etc/newman/report.xml
                '''
            }
        }
    }
     post {
        always {
            // Archive the generated reports for later inspection
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
