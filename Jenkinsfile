pipeline {
    agent any

    stages {    

        stage('Register Security Scan') {
            steps {
                script {
                    if (fileExists("nexus-results.sarif")) {
                        echo "File exists, registering scan..."
                        registerSecurityScan(
                            artifacts: "nexus-results.sarif",
                            format: 'sarif',
                            // scanner: "Anchore",
                            archive: true
                        )
                    } else {
                        error "nexus-results.sarif not found!"
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
        failure {
            echo 'Build or tests failed!'
        }
    }
}
