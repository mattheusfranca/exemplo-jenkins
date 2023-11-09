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
                 sh 'mvn clean test'
                 sh 'mvn surefire-report:report'
            }
        }
        stage ('Build') {
            steps {
                sh 'mvn install -DskipTests -Dquarkus.http.port=8084'
                sh 'docker build -f src/main/docker/Dockerfile.jvm -t udesc/devopsnapratica .'
                sh 'docker login -u ${DOCKER_USER} -p ${DOCKER_PASSWORD}'
                
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

