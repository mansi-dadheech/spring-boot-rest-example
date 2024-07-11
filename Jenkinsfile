
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
	       sh 'mkdir Builds'
	       sh 'cp target/*.jar Builds/spring-boot-app.jar'
	   } 
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("spring-boot-app:v1", "-f Dockerfile .")
                }
            }
        }


    }

}
