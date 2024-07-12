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
            cloudFoundryDeploy script: this,
                cfApiEndpoint: 'https://api.cf.us10-001.hana.ondemand.com',        
                cfOrg: 'e97a1146trial_e97a1146trial',                        
                cfSpace: 'Lokesh',                    
                cfCredentialsId: 'cfCredentialsId',    
                deployType: 'standard',                    
                manifest: 'manifest.yml',
                deployTool: 'mtaDeployPlugin'
        }
    }
}
