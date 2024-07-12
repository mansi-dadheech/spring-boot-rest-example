
pipeline{
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
		sh 'docker build -t spring-boot-app:v1 -f ./CI/Dockerfile'
            }
        }


    }

}
