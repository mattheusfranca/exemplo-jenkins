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
                sh 'docker build -f src/main/docker/Dockerfile.jvm -t mattheushora/udesc .'
                sh 'docker login -u ${DOCKER_USER} -p ${DOCKER_PASSWORD}'
                sh 'docker push mattheushora/udesc'
                
            }
        }
		
        stage ('Deploy/Run') {
            steps {
		echo 'Deploying...'
		dir("/var/jenkins_home/env/dev"){
               	sh 'docker compose down'
                       sh 'docker compose up -d'
                }
            }
        }
		
        stage ('Sonar') {
            steps {
		sh 'mvn sonar:sonar -Dsonar.host.url=http://host.docker.internal:9000 -Dsonar.login=${SONAR_TOKEN}'
	    }
        }
		
    }
}

