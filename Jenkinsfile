pipeline {
    agent any  
    stages {      
        
        stage ('test') {
            steps {
                sh './mvnw test'
            }
        }  
        stage ('package') {
            steps {
                sh './mvnw clean package'
            }
        }   
        stage ('SonarQube analysis') {
     steps {
        script {
           STAGE_NAME = "SonarQube analysis"

              withSonarQubeEnv("SonarGate") {
                sh '/opt/apps/devops/sonar-scanner-4.2.0.1873-linux/bin/sonar-scanner'
              }
           }
        }
     }
  

  stage ('SonarQube Gatekeeper') {
     steps {
        script {
           STAGE_NAME = "SonarQube Gatekeeper"

           if (BRANCH_NAME == "develop") {
              echo "In 'develop' branch, skip."
           }
           else { // this is a PR build, fail on threshold spill
              def qualitygate = waitForQualityGate()
              if (qualitygate.status != "OK") {
                 error "Pipeline aborted due to quality gate duplication failure: ${qualitygate.status}"
              } 
           }
        }
     }
  }     
         
    
                     
        stage ('deploy') {
             steps {
                 sh 'cp target/JPetStore.war /home/dineshreddy99077/noida/apache-tomcat-7.0.103/webapps/'
             }
         }  
         }

}
