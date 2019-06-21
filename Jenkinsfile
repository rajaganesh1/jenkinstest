pipeline {
	agent {label 'pipeline-node'}
	
	environment {
       NEXUS_CREDENTIAL_ID = "nexus-credentials"
    }
	
stages {
        stage('Checkout') {
            steps {
                echo 'Checkout'
            }
        }
	stage('Sonar') {
            steps {
                //echo 'Sonar Scanner'
               	//def scannerHome = tool 'SonarQube Scanner 3.0'
			    //withSonarQubeEnv {
					sh 'mvn sonar:sonar -Dsonar.host.url=http://10.177.168.44:9000'
					//}
	    }
        }
        stage('Build') {
            steps {
                echo 'Clean Build'
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
                sh 'mvn test'
            }
        }
        //stage('JaCoCo') {
            //steps {
               // echo 'Code Coverage'
               // jacoco()
            //}
       // }
        
        stage('Package') {
            steps {
                echo 'Packaging'
                sh 'mvn package -DskipTests'
            }
        }
        stage('Publish to Nexus') {
            steps {
              nexusArtifactUploader(
   	       nexusVersion: 'nexus3',
    	       protocol: 'http',
               nexusUrl: '10.177.168.44:8081/nexus',
               groupId: 'com.artifact',
               version: 0.1,
               repository: 'jenkins-maven',
               credentialsId: 'NEXUS_CREDENTIAL_ID',
          artifacts: [
              [artifactId: projectName,
              classifier: '',
              file: 'springboot-0.0.1.jar',
              type: 'jar']
    ]
 )  
	    }
            }
        }
    }
	}        
