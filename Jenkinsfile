environment {
        PATH = "/usr/local/bin:/opt/homebrew/bin:$PATH"
}

@Library('piper-lib-os') _
node() {
    stage('prepare') {
        checkout scm
        setupCommonPipelineEnvironment script:this
    }
    stage('build') {
        mtaBuild script: this
    }
}
