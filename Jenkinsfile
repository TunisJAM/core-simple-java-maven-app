podTemplate(label: 'kubernetes',                                                                                          
                 containers: [                                                                                            
                 containerTemplate(name: 'maven', image: 'maven:3.5.2-jdk-8-alpine', ttyEnabled: true, command: 'cat')    
                 ]) {

	node('kubernetes') {
	   container('maven') {
		stage('Build') {	
					checkout scm
					sh 'mvn -B -DskipTests clean package'
		}
		stage('Test') {
					sh 'mvn test'
		  post {
			always { 		  	
					junit '**/*.xml'
			}
		  }
		}
		stage('Deliver') {
				sh 'jenkins/scripts/deliver.sh'
		}

		   
	}
	}
		   
		   
}
