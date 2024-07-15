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
        script {
            withEnv(['PATH+MBT=/opt/homebrew/bin']) {
                // Ensure production build to minimize size
                sh 'npm install --production'
                mtaBuild script: this
                // Archive build artifacts
                archiveArtifacts artifacts: '**/target/*.mtar', allowEmptyArchive: true
            }
        }
    }

    stage('deploy') {
        script {
            withEnv(['PATH+CF=/opt/homebrew/bin']) {
                sh 'cf --version'  // Verify CF CLI is available
                pushToCloudFoundry(
                    target: 'https://api.cf.us10-001.hana.ondemand.com',
                    organization: 'e97a1146trial_e97a1146trial',
                    cloudSpace: 'Lokesh',
                    credentialsId: 'LOKESH_SAP_BTP_CRED',
                    pluginTimeout: '3000',  // Set the plugin timeout
                    manifestChoice: [manifestFile: './manifest.yml']
                )
            }
        }
    }
}
