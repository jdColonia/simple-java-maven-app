pipeline {
    agent any
    tools {
	    maven "mavenInstall"
    }
    parameters {
		string(name: 'BRANCH', defaultValue: 'master', description: 'Branch to build')
	}
    stages {
	    stage('Cleanup') {
			steps {
				script {
					if (fileExists('simple-java-maven-app')) {
						echo "Removing existing directory..."
						sh 'rm -rf simple-java-maven-app'
					}
				}
			}
		}
        stage('Clone Repository') {
            steps {
                git 'https://github.com/jenkins-docs/simple-java-maven-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
