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
  

          stage('Quality Gate') {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
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
