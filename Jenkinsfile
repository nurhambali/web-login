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
          steps {
            sh 'echo "INI main"'
          }
        }
      }
		}
	}
  post {
    always {
      archiveArtifacts allowEmptyArchive: true, artifacts: 'index.html', fingerprint: true
    }
  }
}
