pipeline {
    agent any  
    stages {      
        stage ('checkout'){
            steps {
            git  'https://github.com/SAKTHISIVANI18/sonarserver.git'
            }
        }
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
        stage ('sonar') {
            steps {
                sh '/opt/apps/devops/sonar-scanner-4.2.0.1873-linux/bin/sonar-scanner'
            }
        } 
      
        
         stage ('deploy') {
             steps {
                 sh 'cp target/JPetStore.war /home/dineshreddy99077/noida/apache-tomcat-7.0.103/webapps/'
             }
         }  
         }

}
