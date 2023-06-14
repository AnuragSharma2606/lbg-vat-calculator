// This adds a quality gate that aborts the pipeline if the quality threshold isn't met
pipeline {
  agent any

  stages {
    stage('Checkout') {
        steps {
          // Get some code from a GitHub repository
          git branch: 'main', url: 'https://github.com/AnuragSharma2606/lbg-vat-calculator.git'
        }
    }
    stage('SonarQube Analysis') {
      environment {
        scannerHome = tool 'sonarqube'
      }
        steps {
            withSonarQubeEnv('sonarqube-1') {        
              sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 20, unit: 'SECONDS'){
          waitForQualityGate abortPipeline: true
        }
    }
  }
}
}