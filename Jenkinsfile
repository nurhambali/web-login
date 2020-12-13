pipeline {
	agent any
	triggers { pollSCM('* * * * *') }
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
