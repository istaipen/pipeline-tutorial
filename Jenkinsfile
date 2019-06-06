pipeline {
    agent any
    tools {
        maven 'MavenHome'
        jdk 'JDK8'
    }
    stages {
        stage ('Initialize') {
            steps {
                bat '''
                    echo "PATH = %PATH%"
                    echo "M2_HOME = %M2_HOME%"
                '''
            }
        }

        stage ('Build') {
            steps {
                    bat 'cd NumberGenerator & mvn install'
            }
             post {
                success {
                    junit 'NumberGenerator/target/surefire-reports/*.xml'
                        }
                 }
        }
		
		stage('Sonarqube') {
			environment {
				scannerHome = tool 'sonarQube'
			}

			steps {
				withSonarQubeEnv('sonarqube') {
					bat "${scannerHome}/bin/sonar-scanner"
				}

				timeout(time: 10, unit: 'MINUTES') {
					waitForQualityGate abortPipeline: true
				}
			}
		}
    }
    
}
