pipeline{
	agent any
	stages{
		stage("Pull Latest Image"){
			steps{
				bat "docker pull affanr/selenium-docker"
			}
		}
		//Here we run the grid seperately
		//using the -d command we run it in the background
		//And only select the Hub, Chrome, and Firefox images to run from the docker-compose file		
		stage("Start Grid"){
			steps{
				bat "docker-compose up -d hub chrome firefox" 
			}
		}
		//We then run the test images seperately 
		stage("Run Test"){
			steps{
				bat "docker-compose up search-module"
			}
		}
	}
	//This post command always runs even if we kill the job.
	//Here we are saying to archive the test results in the slaves workspace directory
	post{
		always{
			archiveArtifacts artifacts: 'output/**' //archive everything under output folder
			bat "docker-compose down" //we put the down command here so even if we kill the job the grid will be brought down successfully
			bat "rmdir /s /q %WORKSPACE%\\output"
		}
	}
}
