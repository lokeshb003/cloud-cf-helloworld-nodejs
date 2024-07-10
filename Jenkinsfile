pipeline {
    agent any
    stages {
        stage('Setup') {
            steps {
                script {
                    sh 'curl --insecure --silent --retry 5 --retry-max-time 240 --location --output piper https://github.com/SAP/jenkins-library/releases/download/v1.369.0/piper-darwin.arm64'
                    sh 'chmod +x piper'
                    sh './piper version'
                }
            }
        }
        stage('Build with Piper') {
            steps {
                script {
                    sh 'brew install mbt'
                    sh './piper mtaBuild'
                }
            }
        }
    }
}
