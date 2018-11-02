podTemplate(label: 'kubernetes',                                                                                          
                 containers: [                                                                                            
                 containerTemplate(name: 'maven', image: 'maven:3.5.2-jdk-8-alpine', ttyEnabled: true, command: 'cat')    
                 ]) {


		stage('Build') {
		  steps {
		        node('kubernetes') {
				container('maven') {
					sh 'mvn -B -DskipTests clean package'
				}
				}
		  }
		}
		stage('Test') {
		  steps {
		  		node('kubernetes') {
				container('maven') {
					sh 'mvn test'
				}
				}
		  }
		  post {
			always { 
		  		node('kubernetes') {
				container('maven') {
					junit '**/*.xml'
				}
				}
			}
		  }
		}
		stage('Deliver') {
		  steps {
			node('kubernetes') {
			container('maven') {
				sh 'jenkins/scripts/deliver.sh'
			}
			}
		  }
		}

}
