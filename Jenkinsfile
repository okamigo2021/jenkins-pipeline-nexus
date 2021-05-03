pipeline {
    agent any
    tools {
        maven 'maven3'
    }

    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                script{

                    nexusArtifactUploader artifacts: [
					    [
						    artifactId: 'simple-app', 
							classifier: '', 
                            file: 'target/simple-app-1.0.0.war', 
							type: 'war'
							]
						], credentialsId: 'e0850b2e-0788-4e40-bf42-53edd03c69b1', 
						   groupId: 'in.javahome', 
						   nexusUrl: 'localhost:8081', 
						   nexusVersion: 'nexus3', 
						   protocol: 'http', 
						   repository: 'http://192.168.1.172:8081/repository/maven-nexus-repo', 
						   version: '1.0.0'
                    }
            }
        }
    }
}