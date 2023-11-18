@Library('my-shared-library') _

pipeline{
  agent any
    stages{
      stage('GIT Checkout'){
           when { expression { params.action == 'create'} }
          steps{
          gitCheckout(
            branch: "main",
            url: "https://github.com/sandeepnainala/Java_app.git"
          )
          }
        }
      stage('Unit test'){
         when { expression { params.action == 'create'} }
        steps{
          scripts{
            mvnTest()
          }
        }
      }
      stage('Intergration Test Maven'){
      when { expression { params.action == 'create'} }
        steps{
          scripts{
            mvnIntegrationTest()
          }
        }
      }
      stage('Static Code analysis: Sonarqube'){
      when { expression { params.action == 'create'} }
        steps{
          scripts{
            def SonarQubecredentialsId = 'sonar-api'
            staticCodeAnalysis(SonarQubecredentialsId)
          }
        }
      }
      stage('Quality Gate Status Check: Sonarqube'){
      when { expression { params.action == 'create'} }
        steps{
          scripts{
            def SonarQubecredentialsId = 'sonar-api'
            QualityGateStatus(SonarQubecredentialsId)
          }
        }
      }
    }
}