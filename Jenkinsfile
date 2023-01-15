pipeline {
  agent any
  stages {
    
    stage ('test') { // la phase build
        steps {
        dir('sub-dir') {bat 'gradlew.bat clean test'}
               }
        }
  }
}
