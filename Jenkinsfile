pipeline {
  agent any
    tools {
      maven 'maven3'
                 jdk 'JDK8'
    }
    stages {      
        stage('Build maven ') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 def customImage = docker.build('singam1234/petclinic', "./docker")
                 docker.withRegistry('https://hub.docker.com/', 'singam1234') {
                 customImage.push("${env.BUILD_NUMBER}")
                 }                     
           }
        }
	  }
    }
}
