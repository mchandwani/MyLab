pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
     environment {
       ArtifactId = readMavenPom().getArtifactId()
       Version = readMavenPom().getVersion()
       Name = readMavenPom().getName()
       GroupId = readMavenPom().getGroupId()
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

          // Stage 4 : Print some information
        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
                }

        // Stage3 : Publish the source code to SNexus
         stage ('Publish to Nexus'){
            steps {
                echo 'Publishine.....'
                script
                {
                     def NexusRepo = Version.endsWith("SNAPSHOT") ? "MukeshDevOpsLab-SNAPSHOT" : "MukeshDevOpsLab-RELEASE"
                    nexusArtifactUploaderartifacts: 
                    [[
                        artifactId: "${ArtifactId}",
                        classifier: '',
                        file: "target/${ArtifactId}-${Version}.war",
                        type: 'war'
                    ]],
                    credentialsId: 'c50b85e4-316a-4e9a-b6c6-0e4c1dc631f9',
                    groupId: "${GroupId}",
                    nexusUrl: '172.20.10.168:8081',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: "${NexusRepo}",
                    version: "${Version}"           
                }
            }
        }
             
        
    }

}