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
                    bat 'cd NumberGenerator & mvn clean install'
            }         
        }
		
	    stage ('JUNIT Test'){
			steps{
					bat 'cd NumberGenerator & mvn clean install'
			}
			post {
					success {
						junit 'NumberGenerator/target/surefire-reports/*.xml'
							}
			}
		}
		
		stage ('Sonar Code') {
            steps {
                bat 'cd NumberGenerator & mvn -DskipTests sonar:sonar -Dsonar.host.url=http://localhost:9008 -Dsonar.login=admin -Dsonar.password=admin'
            }
        }
		

    }
    
}
