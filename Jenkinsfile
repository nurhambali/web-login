pipeline {
	agent none
	stages {
		stage('COPY FILE'){
			steps([$class: 'BapSshPromotionPublisherPlugin']){
				sshPublisher(
					continueOnError: false, failOnError: true,
					publishers: [
						sshPublisherDesc(
							configName: "server-01",
							verbose: true,
							transfers: [
								sshTransfer(execCommand: "systemctl stop metricbeat"),
								sshTransfer(execCommand: "cd /tmp", sourceFiles: "**", )
							]
						)
					]
				)
			}
		}
	}
}