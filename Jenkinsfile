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
                   withSonarQubeEnv(credentialsId: 'sonarqube') {
                     sh 'chmod +x gradlew'
                     sh ' ./gradlew sonarqube'
                   }
            
                }
            }

        }
    }
}