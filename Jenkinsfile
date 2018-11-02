podTemplate(label: 'kubernetes',                                                                                          
                 containers: [                                                                                            
                 containerTemplate(name: 'maven', image: 'maven:3.5.2-jdk-8-alpine', ttyEnabled: true, command: 'cat')    
                 ]) {


		stage('Build') {

		        node('kubernetes') {
				container('maven') {
					sh 'mvn -B -DskipTests clean package'
				}
				}

		}
		stage('Test') {

		  		node('kubernetes') {
				container('maven') {
					sh 'mvn test'
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

			node('kubernetes') {
			container('maven') {
				sh 'jenkins/scripts/deliver.sh'
			}
			}

		}

}
