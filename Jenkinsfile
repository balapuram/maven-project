pipeline {
agent any

	stages {
		stage ('Build'){
			steps {
				sh 'mvn clean package'
			}
			post {
				success {
					echo 'Now Archiving'
					archiveArtifacts artifacts: '**/target/*.war'
				}
			}
		}
		stage ('Deploy to stage'){

			steps {
				build 'deploy-to-stage'
			}
		}

		stage ('Deploy to Production'){

			steps {

				timeout (time:5, unit: 'DAYS'){
					input message: "Aprrove PRODUCTION Deployment"
				}

				build 'deploy-to-prod'
			}
			post{
				success{
					echo 'code deployed successfully'
					
				}
				failure{
					echo 'code not deployed correctly'
				}

			}

		
		}
	}
}
