pipeline {
	agent any
	triggers { pollSCM('* * * * *') }
  options {
    buildDiscarder(logRotator(numToKeepStr: '3', artifactNumToKeepStr: '3', daysToKeepStr: '3'))
    timestamps()
    ansiColor('xterm')
    disableResume()
    durabilityHint('PERFORMANCE_OPTIMIZED')
    rateLimitBuilds(throttle: [count: 60, durationName: 'hour', userBoost: true])
    quietPeriod(10)
  }
	stages {

    stage('Build') {
      steps {
        sh 'echo "Build"'
      }
    }
    stage('Delivery') {
      failFast true
      parallel {
        stage('Demo') {
          when {
            branch 'demo'
          }
          steps {
            sh 'echo "INI DEMO"'
          }
        }
        stage('Prodaction') {
          when {
            branch 'main'
          }
        steps([$class: 'BapSshPromotionPublisherPlugin']) {
        sshPublisher(
          continueOnError: false, failOnError: true,
          publishers: [
          sshPublisherDesc(
           configName: "server-01",
           verbose: true,
           transfers: [
            ssTransfer(
              sourceFiles:"**",
              remoteDirectory: "/tmp",
              execCommand: "systemctl restart nginx"
              )])]
          )
        }
      }
		}
	}}
  post {
    always {
      archiveArtifacts allowEmptyArchive: true, artifacts: 'index.html', fingerprint: true
    }
  }
}
