pipeline{
   agent{
        docker {
              image 'maven:3-alpine'
              args  '-e http_proxy=web-proxy.ap.softwaregrp.net:8080 -e https_proxy=web-proxy.ap.softwaregrp.net:8080 -v /root/.m2/:/root/.m2 -v /home/buildmymaven/settings.xml:/root/.m2/settings.xml:ro'
        }
    }
    stages{
         stage('Build'){
              steps{
                   sh 'mvn -B -DskipTests clean package'
              }
         }
         stage('Test'){

            steps{
               sh 'mvn test'
            } 
            post{
              always{
                 junit 'target/surefile-reports/*.xml'
              }
           }      
        }
    }
}
