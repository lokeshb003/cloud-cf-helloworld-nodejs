pipeline {
    agent any
    environment {
        PATH = "/usr/local/bin:/opt/homebrew/bin:$PATH"
    }
    stages {
        stage('Setup') {
            steps {
                script {
                    sh 'curl --insecure --silent --retry 5 --retry-max-time 240 --location --output piper https://github.com/SAP/jenkins-library/releases/download/v1.370.0/piper_master'
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
                    sh 'mbt --version'
                    sh './piper mtaBuild'
                }
            }
        }
        stage('Deploy to CloudFoundry') {
            steps {
                script {
                    sh './piper cloudFoundryDeploy --deployTool="mtaDeployPlugin" --deployType="standard" --apiEndpoint="https://api.cf.us10-001.hana.ondemand.com" --org="e97a1146trial_e97a1146trial" --space="Lokesh" --username="lokesh.b.2020.ad@ritchennai.edu.in" --password="tofsYz-roqrit-8jyxga"'
                }
            }
        }
        stage('Archive Artifact') {
            steps {
                script {
                    // Archive the generated MTAR artifact
                    archiveArtifacts artifacts: '**/*.mtar', allowEmptyArchive: true
                }
            }
        }
    }
}
