pipeline {
	agent {label 'pipeline-node'}
		
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
                echo '## TODO DEPLOYMENT ##'
            }
        }
    }
	}
    
    post {
        always {
            echo 'JENKINS PIPELINE'
        }
        success {
            echo 'JENKINS PIPELINE SUCCESSFUL'
        }
        failure {
            echo 'JENKINS PIPELINE FAILED'
        }
        unstable {
            echo 'JENKINS PIPELINE WAS MARKED AS UNSTABLE'
        }
        changed {
            echo 'JENKINS PIPELINE STATUS HAS CHANGED SINCE LAST EXECUTION'
        }
    }
