pipeline{
	agent any
	stages{
		stage("Pull Latest Image"){
			steps{
				bat "docker pull affanr/selenium-docker"
			}
		}
		stage("Start Grid"){
			steps{
				bat "docker-compose up -d hub chrome firefox" //This command tells docker to start the hub, chrome, and firefox servicec only. -d says to start them in the back ground. Removing -d will put the jenkins job in an endless loop since the selenium grid will keep on running and listening.
			}
		}
		stage("Run Test"){
			steps{
				bat "docker-compose up search-module"
			}
		}
	}
	post{
		always{
			archiveArtifacts artifacts: 'output/**'
			bat "docker-compose down"
			bat "rmdir /s /q %WORKSPACE%\\output"
		}
	}
}
