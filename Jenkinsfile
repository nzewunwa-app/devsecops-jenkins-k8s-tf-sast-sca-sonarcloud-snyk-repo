pipeline {
  agent any

  tools { 
    maven 'Maven 3.9.9'
  }

  stages {

    stage('CompileandRunSonarAnalysis') {
      steps {
        bat '''
          mvn clean verify sonar:sonar \
            -Dsonar.projectKey=zesgbuggywebapp_zesgbuggywebapp \
            -Dsonar.organization=zesgbuggywebapp \
            -Dsonar.host.url=https://sonarcloud.io \
            -Dsonar.token=9fd18d34333de4fd2510f5e505fd9cf80ef02397
        '''
      }
    }

    stage('RunSCAAnalysisUsingSnyk') {
      steps {
        withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
          bat '''
            mvn snyk:test -fn
          '''
        }
      }
    }

  }
}
