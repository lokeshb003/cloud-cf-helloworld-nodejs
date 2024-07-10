pipeline {
    agent {
        docker {
            image 'ppiper/cf-cli' 
            args '-u root:root'
        }
    }
    @Library('piper-lib-os')
    stages {
        stage('prepare') {
          checkout scm
          setupCommonPipelineEnvironment script:this
        }
    }
        
