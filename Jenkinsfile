@Library('piper-lib-os') _
node() {
    stage('prepare') {
        checkout scm
        setupCommonPipelineEnvironment script:this
        sh 'chmod +x ./piper'
    }
    stage('build') {
        mtaBuild script: this
    }
}
