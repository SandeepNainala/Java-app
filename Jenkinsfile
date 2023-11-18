@Library('my-shared-library') _

pipeline{
  agent any
  parameters {
  choice(name: 'action', choices: 'create/delete', description: 'Choose create/Destroy')
  string(name: 'ImageName', defaultValue: 'name of the docker build', description: 'javapp')
  string(name: 'ImageTag', defaultValue: 'tag of the docker build', description: 'v1')
  string(name: 'DockerHubUser', defaultValue: 'name of the docker Application', description: 'sandeepnainala9')
  }
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
      stage('Docker Image Scan: trivy'){
      when { expression { params.action == 'create'} }
        steps{
          script{
            dockerImageScan("${params.ImageName}", "${params.ImageTag}", "${params.DockerHubUser}")
          }
        }
      }
      stage('Docker Image Push: DockerHub'){
      when { expression { params.action == 'create'} }
        steps{
          script{
            dockerImagePush("${params.ImageName}","${params.ImageTag}", "${params.DockerHubUser}")
          }
        }
      }
      stage('Docker Image CleanUp: DockerHub'){
      when { expression { params.action == 'create'} }
        steps{
          script{
            dockerImageCleanUp("${params.ImageName}", "${params.ImageTag}", "${params.DockerHubUser}")
          }
        }
      }
    }
  }