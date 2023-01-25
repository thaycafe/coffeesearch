pipeline{
    agent any
    
    stages{
        stage('Clone do Codigo'){
            steps{
                git url: 'https://github.com/thaycafe/4coffee-app'
            }
        }

        stage('SAST com Sonarqube'){
            environment {
                scanner = tool 'sonar-scanner'
            }
            steps{
                withSonarQubeEnv('sonarqube') {
                    sh "${scanner}/bin/sonar-scanner -Dsonar.projectKey=4coffee -Dsonar.sources=${WORKSPACE}/ -Dsonar.projectVersion=${BUILD_NUMBER}"
                }
                waitForQualityGate abortPipeline: true
            }
            
        }
        
    }

    post {
        success {
            echo "Pipeline executado com sucesso!!"
        }
        failure {
            echo "Pipeline falhou!"
        }
    }
}
