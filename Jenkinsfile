pipeline {
	agent {
		dockerfile {
			label 'docker'
			// image 'python:3'
		}
	}
	stages {
		stage('Compile') {
			steps {
				sh 'python3 -m compileall subtractor.py'
			}
		}
		stage('Run') {
			steps {
				sh 'python3 subtractor.py 3 5'
			}
		}
		stage('Unit test') {
			steps {
				sh '''python3 -m pytest \
					-v --junitxml=junit.xml \
					--cov-report xml --cov subtractor subtractor.py
				'''
			}
		}
	}
	post {
		always {
			junit 'junit.xml'
			cobertura coberturaReportFile: 'coverage.xml'
		}
	}
}