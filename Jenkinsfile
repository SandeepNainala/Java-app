pipeline{
  agent any
    stages{
      stage('GIT Checkout'){
        steps{
        gitCheckout(
          branch: "main",
          url:    "https://github.com/SandeepNainala/Java-app.git"
        )
        }
      }
      stage('Unit test'){
        steps{
          scripts{
            mvnTest()
          }
        }
      }

    }
}