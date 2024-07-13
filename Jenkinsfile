
pipeline {
    agent any

    tools {
	maven 'Maven'
    }

    stages {
        stage('Build'){
	   steps {
               sh 'mvn clean package'
           }
	   post{
	      success{
	       archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
	      }
	   }
	}

        stage('Prepare Artifacts'){
           steps {
	       sh 'cp target/*.jar Builds/spring-boot-app.jar'
	   } 
        }

        stage('Build Docker Image') {
            steps {
		sh 'docker build -t spring-boot-app:v1 -f ./CI/Dockerfile .'
            }
        }

	stage('Push image') {
            steps {
                script {
	           sh "docker tag spring-boot-app:v1 mansi22/spring-boot-app:v1"		
                   docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                       def app = docker.image("mansi22/spring-boot-app:v1")
                       app.push()
                   }
	        }
	    }

    }
}
}
	

