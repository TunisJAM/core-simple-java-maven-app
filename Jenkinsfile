podTemplate(label: 'kubernetes',                                                                                          
                 containers: [                                                                                            
                 containerTemplate(name: 'maven', image: 'maven:3.5.2-jdk-8-alpine', ttyEnabled: true, command: 'cat')    
                 ]) {
    stages {
      node('kubernetes') {                                                                                         
      container('maven') {
		stage('Build') {
		  steps {
			sh 'mvn -B -DskipTests clean package'
		  }
		}
		stage('Test') {
		  steps {
			sh 'mvn test'
		  }
		  post {
			always { 
			  junit '**/*.xml'
			}
		  }
		}
		stage('Deliver') {
		  steps {
			sh 'jenkins/scripts/deliver.sh'
		  }
		}
   }
}
