@Library('piper-lib-os') _
node {
    environment {
        PATH = "/usr/local/bin:/opt/homebrew/bin:/usr/local/go/bin:$PATH"
    }

    stage('prepare') {
        checkout scm
        setupCommonPipelineEnvironment script: this
    }

    stage('build') {
        withEnv(['PATH+MBT=/opt/homebrew/bin']) {
            mtaBuild script: this
            // Archive build artifacts
            archiveArtifacts artifacts: '**/target/*.*', allowEmptyArchive: true
        }
    }

    stage('deploy') {
        withEnv(['PATH+CF=/opt/homebrew/bin']) {
            sh 'cf --version'  // Verify CF CLI is available
            sh 'cf login -u lokesh.b.2020.ad@ritchennai.edu.in -p Bewboh-diwjY1-minsuh'
            sh 'cf push -f manifest.yml'
        }
    }
}
