pipeline {
    agent any

    stages {    
        // stage('Registering build artifact') {
        //     steps {
        //         echo 'Registering the metadata'
        //         registerBuildArtifactMetadata(
        //             name: "test-artifact-demo",
        //             version: "1.0.1",
        //             type: "docker",
        //             url: "http://non:1111",
        //             digest: "6f637064707039346163663237383938",
        //             label: "prod"
        //         )
        //     }
        // }

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
