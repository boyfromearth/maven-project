pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
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
		stage ('Deploy to Production'){
            steps{
				timeout(time:5, unit:'DAYS'){
					input message:'Appprove Production deployment'
					
					}
                build job: 'Deploy_To_Prod'
            }
			post{
				success {
					echo 'Code Deployment to Production'
					}
				failure {
					echo 'Deployment failed'
				}	
			}
		}
	}
}