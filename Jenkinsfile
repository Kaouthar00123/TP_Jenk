pipeline {
  agent any
  stages {
    
    
      stage ('test') { 
          steps { 
              bat 'gradlew test'
              archiveArtifacts 'build/reports/tests/test/*'
              cucumber reportTitle: 'My report', fileIncludePattern: '*/.json'
                 
          }
      }     
      
    
    
    stage('SonarQube analysis') {
             
      steps {                       
              withSonarQubeEnv('sonar') {
                 bat 'gradle sonarqube'
              }
                             
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
          //slackSend( channel: "#OGL_PROJECT", token: "wMNmqJHk7RxqY92qkHn52aOJzaecMKqe", color: "good", message: "Test Email")
             mail to: "jk_essaheli@esi.dz",
                       subject: "Test Email",
                       body: "Test"
            echo 'This will run only if successful'
        }
        failure {
          //slackSend( channel: "#OGL_PROJECT", token: "wMNmqJHk7RxqY92qkHn52aOJzaecMKqe", color: "good", message: "Test Email fail")
             //mail to: "jk_essaheli@esi.dz",
                      // subject: "Test Email fail",
                      // body: "Test"
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
