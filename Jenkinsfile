pipeline {
	agent any
	stages {
		stage(build){
			steps{				
				sh "mvn clean package"
			}
			post{
				success{
					echo "now archiving..."
					archiveArtifacts artifacts: '**/target/*.war'
				}
			}
		}
		
	}
}
