pipeline {

    agent any

     
    stages {
        
        stage ('checkout'){
            steps {
            git  'https://github.com/SAKTHISIVANI18/sonarserver.git'
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
        
        
     
        

    }
}
