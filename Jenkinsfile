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
        withEnv(['PATH+MBT=/opt/homebrew/bin']) {
            mtaBuild script: this
        }
    }
    stage('deploy') {
        withEnv(['PATH+CF=/opt/homebrew/bin']) {
            cloudFoundryDeploy script: this,
                    cfApiEndpoint: 'https://api.cf.us10-001.hana.ondemand.com',        
                    cfOrg: 'e97a1146trial_e97a1146trial',                        
                    cfSpace: 'Lokesh',                    
                    cfCredentialsId: 'cfCredentialsId',    
                    deployType: 'standard',                    
                    manifest: 'manifest.yml',
                    deployTool: 'cf_native'
        }
    }
}
