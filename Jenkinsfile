pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage3 : Publish the source code to SNexus
         stage ('Publish to Nexus'){
            steps {
                echo 'Publishine.....'
                nexusArtifactUploader artifacts: [[artifactId: 'TestDevOpsLab', classifier: '', file: 'target/TestDevOpsLab.0.0.2.war', type: 'war']], credentialsId: 'c50b85e4-316a-4e9a-b6c6-0e4c1dc631f9', groupId: 'com.testdevopslab', nexusUrl: '172.20.10.168:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'MukeshDevOpsLab-RELEASE', version: '0.0.2'
            }
        }
             
        
    }

}