podTemplate(label: 'kubernetes',                                                                                          
                 containers: [                                                                                            
                 containerTemplate(name: 'maven', image: 'maven:3.5.2-jdk-8-alpine', ttyEnabled: true, command: 'cat')   ,
                 containerTemplate(name: 'maven-java-11', image: 'maven:3.5.4-jdk-11-slim', ttyEnabled: true, command: 'cat')                     
                 ]) {

	node('kubernetes') {
	   container('maven-java-11') {
		stage('Build') {	
					checkout scm
					sh 'mvn -B -DskipTests clean package'
		}
		stage('Test') {
					sh 'mvn test'
				        junit '**/*.xml'
		
		}
		stage('Deliver') {
				sh 'jenkins/scripts/deliver.sh'
		}

		   
	}
	}
		   
		   
}
