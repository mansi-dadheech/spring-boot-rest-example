
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


    }

}
