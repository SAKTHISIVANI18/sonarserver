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
                 withSonarQubeEnv('sonarqube') {
                sh '/opt/apps/devops/sonar-scanner-4.2.0.1873-linux/bin/sonar-scanner'
                       }
        timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
            }
        } 
      
        }
        timeout(time: 10, unit: 'MINUTES') {
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
