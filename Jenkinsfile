pipeline {
  agent any
  stages {
    
    
      stage ('test') { 
          steps { 
              bat 'gradle test'
              bat 'gradle assemble'
          }
      }     
      
    
    
    stage('SonarQube analysis') {
               steps {
                             
                  }
  
        }
        
    
    
    
        stage ('Quality') { 
                steps { 
                              timeout(time: 1, unit: 'HOURS') {
                              waitForQualityGate abortPipeline: true
                            }

                }
        }
                
          
          
          
          stage ('build') { 
                steps { 
                  bat 'gradle build'
                }

          }           
            
            stage ('deploy') { 
                  steps { 
                    bat 'gradle publish'
                  }
            }              
              
              stage ('notify') { 
                steps { 
                     echo 'hello'
                   }
                }

      
}
              
                 post {
       
        success {
             mail to: "jk_essaheli@esi.dz",
                       subject: "Test Email",
                       body: "Test"
            echo 'This will run only if successful'
        }
        failure {
             mail to: "jk_essaheli@esi.dz",
                       subject: "Test Email fail",
                       body: "Test"
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
        }
    }

}
