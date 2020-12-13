pipeline {
	agent any
	triggers { pollSCM('* * * * *') }
	stages {
    stage('Delivery') {
      parallel {
        failFast true
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
