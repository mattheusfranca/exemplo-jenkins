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
                sh 'mvn clean install -Dmaven.test.skip=true  -Dquarkus.http.port=8084'
            }
        }
		
        stage ('Deploy') {
            steps {
					echo 'Deploying...'
            }
        }
		
        stage ('Sonar') {
            steps {
			     sh 'mvn sonar:sonar -Dsonar.host.url=http://host.docker.internal:9000 -Dsonar.login=9c4e300f094dd343742f7cc59703d9863c6b1644'
			}

        }
		
    }
}

