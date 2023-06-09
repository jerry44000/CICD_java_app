@Library('my-shared-library') _

pipeline{
    agent any

    stages {
        stage('Git Checkout'){
            steps{
                    gitCheckout(
                        branch: "main",
                        url: "https://github.com/jerry44000/CICD_java_app.git"
                    )             
            }
            
        }
        stage('Unit Test Maven'){
                steps {
                    script {
                        mvnTest()
                    }
                }
            }
    }
}