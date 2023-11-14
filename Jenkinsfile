pipeline{
  agent any
    stages{
      stage('GIT Checkout'){
        steps{
          git branch: 'main', url: 'https://github.com/SandeepNainala/Java-app.git'
        }
      }
      stage('Unit test'){
        steps{
          scripts{
            sh 'mvn test'
          }
        }
      }
      stage('Intergration Test Maven'){
        steps{
          scripts{
            sh 'mvn verify -DskipUnitTests'
          }
        }
      }

    }
}