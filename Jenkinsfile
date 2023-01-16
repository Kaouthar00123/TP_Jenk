pipeline {
  agent any
  stages {
    
    
      stage ('test') { 
          steps { 
              bat 'gradlew test'
              junit 'build/test-results/**/*.xml'
              cucumber reportTitle: 'My report', fileIncludePattern: 'target/report.json'
                 
          }
      }     
      
    
    
    stage('SonarQube analysis') {
             
      steps {                       
              withSonarQubeEnv('sonar') {
                 bat 'gradlew sonar'
              }
                             
      }
  
        }
        
    
    
    
        /*stage ('Quality') { 
                steps { 
                              timeout(time: 1, unit: 'HOURS') {
                              waitForQualityGate abortPipeline: true
                            }

                }
        } */
                
          
          
          
          stage ('build') { 
            steps { 
              bat 'gradlew build'
              bat 'gradlew javadoc'
              archiveArtifacts 'build/libs/*.jar'
              archiveArtifacts 'build/docs/javadoc/*'
            }
            
          }           
            
            stage ('deploy') { 
                  steps { 
                    bat 'gradlew publish'
                  }
            }              
              
              stage ('notify') { 
                steps { 
                     echo 'hello from jenkins'
                   }
                }

      
}
              
               post {
       
        success {
          
          notifyEvents message: 'Success <b>Hello</b>', token: 'wMNmqJHk7RxqY92qkHn52aOJzaecMKqe'
             mail to: "jk_essaheli@esi.dz",
                       subject: "Test Email",
                       body: "Test"
            echo 'This will run only if successful'
          
        }
        failure {
         
           notifyEvents message: 'Fail <b>Hello</b>', token: 'wMNmqJHk7RxqY92qkHn52aOJzaecMKqe'
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
