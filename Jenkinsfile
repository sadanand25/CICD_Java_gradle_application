pipeline{
    agent any
    stages{
        stage("Sonar Qube quality check"){
            agent{
                docker{
                    image 'openjdk:11'
                }
            }
            steps{
                script{
                   withSonarQubeEnv(credentialsId: 'sonar') {
                     sh 'chmod +x gradlew'
                     sh './gradlew sonarqube -Dsonar.host.url=http://192.168.56.12:9000 -Dsonar.java.binaries=/etc/sonarqube'
                   }
                   timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }

                }
            }

        }
    }
}