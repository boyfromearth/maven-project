pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                call 'mvn clean'
                call 'mvn package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Staging'){
            steps{
                build job: 'Deploy_To_Staging'
            }
        }
    }
}