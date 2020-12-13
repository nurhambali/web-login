pipeline {
	agent any
	triggers { pollSCM('* * * * *') }
	stages {
    stage('Delivery') {
      failFast true
      parallel {
        stage('Demo') {
          when {
            branch 'demo'
          }
          steps {
            sh 'echo "INI DEMO" '
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
}
