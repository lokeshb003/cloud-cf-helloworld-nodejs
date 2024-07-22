@Library('piper-lib-os') _
node() {
    stage('prepare') {
        checkout scm
        setupCommonPipelineEnvironment script: this
    }
    stage('build') {
        withEnv(['PATH+MBT+DOCKER=/opt/homebrew/bin']) {
            mtaBuild script: this
        }
    }
    stage('deploy') {
        withEnv(['PATH+CF=/opt/homebrew/bin']) {
            cloudFoundryDeploy script: this
        }
    }
}
