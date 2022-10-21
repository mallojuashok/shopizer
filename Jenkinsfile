pipeline {
    agent { label 'MY-LABEL-UBUNTU' }
    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'clean install', description: 'maven goal')

    }
    stages{
        stage('VCS'){
            steps{
                git branch: "Test", url: 'https://github.com/mallojuashok/shopizer.git'
            }
        }
        stage ('Artifactory configuration') {
            steps {
                
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "My_Frog",
                    releaseRepo: 'shzr-libs-release-local',
                    snapshotRepo: 'shzr-libs-snapshot-local'
                )


            }
        }
        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'MVN_DEFAULT', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER"
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "My_Frog"
                )
            }
        }


    }
}