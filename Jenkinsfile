pipeline {
    agent any 
	tools { 
        maven 'Maven' 
    }   
    stages {
        stage ('Initialize') {
            steps {
                 echo 'Inciando...'
            }
        }

       stage ('Test') {
            steps {
                 sh 'mvn test'
            }
        }
        stage ('Build') {
            steps {
                sh 'mvn clean install -Dquarkus.http.port=8084'
            }
        }
		
        stage ('Deploy') {
            steps {
		echo 'Deploying...'
            }
        }
		
        stage ('Sonar') {
            steps {
		sh 'mvn sonar:sonar -Dsonar.host.url=http://host.docker.internal:9000 -Dsonar.login=${SONAR_TOKEN}'
	    }
        }
		
    }
}

