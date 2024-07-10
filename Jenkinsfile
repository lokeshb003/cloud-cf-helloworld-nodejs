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
                    sh 'curl -L -o cloud-mta-build-tool_1.2.30_Darwin_arm64.tar.gz https://github.com/SAP/cloud-mta-build-tool/releases/download/v1.2.30/cloud-mta-build-tool_1.2.30_Darwin_arm64.tar.gz'
                    sh 'tar xvzf cloud-mta-build-tool_1.2.30_Darwin_arm64.tar.gz'
                    sh 'mv mbt /usr/local/bin/'
                    sh './piper mtaBuild'
                }
            }
        }
    }
}
