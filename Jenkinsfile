pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    // Download the binary
                    sh 'curl --insecure --silent --retry 5 --retry-max-time 240 --location --output piper https://github.com/SAP/jenkins-library/releases/download/v1.369.0/piper-darwin.arm64'
                    // Make it executable
                    sh 'chmod +x piper'
                    // Check version
                    sh './piper version'
                }
            }
        }
    }
}
