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
          script{
            mvnTest()
          }
        }
      }
      stage('Intergration Test Maven'){
      when { expression { params.action == 'create'} }
        steps{
          script{
            mvnIntegrationTest()
          }
        }
      }
      stage('Static Code analysis: Sonarqube'){
      when { expression { params.action == 'create'} }
        steps{
          script{
            def SonarQubecredentialsId = 'sonar-api'
            staticCodeAnalysis(SonarQubecredentialsId)
          }
        }
      }
      stage('Quality Gate Status Check: Sonarqube'){
      when { expression { params.action == 'create'} }
        steps{
          script{
            def SonarQubecredentialsId = 'sonar-api'
            QualityGateStatus(SonarQubecredentialsId)
          }
        }
      }
      stage('Maven Build : Maven'){
      when { expression { params.action == 'create'} }
        steps{
          script{
            mvnBuild()
          }
        }
      }
      stage('Docker Image Build'){
      when { expression { params.action == 'create'} }
        steps{
          script{
            dockerBuild("${params.ImageName}", "${params.ImageTag}", "${params.DockerHubUser}")
          }
        }
      }
    }
}