pipeline{

      agent {
                docker {
                image 'maven'
		args '-v ${user.home}/.m2:/root/.m2'

                }
            }
        
        stages{

              stage('Quality Gate Status Check'){
                  steps{
                      script{
			      withSonarQubeEnv('sonarqubeserver') { 
			      sh "mvn clean sonar:sonar"
                       	     	}
			      timeout(time: 2, unit: 'MINUTES') {
			      def qg = waitForQualityGate()
				      if (qg.status != 'OK') {
					   error "Pipeline aborted due to quality gate failure: ${qg.status}"
				      }
                    		}
		    	    sh "mvn clean install"
		  
                 	}
               	 }  
              }	
		
            }	       	     	         
}
