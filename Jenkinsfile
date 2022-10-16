pipeline {
    agent { label 'TerraformLabel' }
     triggers {
        pollSCM('30 5 * * *')
    }
    stages{
        stage('VCS'){
            steps{
                git branch:'release', url:'https://github.com/mallojuashok/shopizer.git'
            }
        }
        stage('build'){
            steps{
                sh '/usr/share/maven/bin/mvn package'
            }
        }
        stage('archive results'){
            steps{
                junit '**/surefire-reports/*.xml'
            }
        }
        stage('artifacts'){
            steps{
                archiveArtifacts artifacts: '**/target/*.jar'
            }
        }
        
    }

    }