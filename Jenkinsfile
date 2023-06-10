@Library('my-shared-library') _

pipeline{
    agent any

    parameters {
        choice(name: 'action', choices:'create\ndelete', description: 'Choose create/destroy')
    }

    stages {

        stage('Git Checkout'){

        when { expression { param.action == 'create'} }
        
            steps{
                    gitCheckout(
                        branch: "main",
                        url: "https://github.com/jerry44000/CICD_java_app.git"
                    )             
            }
            
        }
        stage('Unit Test Maven'){

        when { expression { param.action == 'create'} }

                steps {
                    script {
                        mvnTest()
                    }
                }
            }
        stage('Integration Test Maven'){

        when { expression { param.action == 'create'} }

                steps {
                    script {
                        mavenIntegration()
                    }
                }
            }
        stage('Sonarqube Static Code Analysis'){

        when { expression { param.action == 'create'} }

               steps {
                  script {
                    staticCodeAnalysis()
                  }
               }  
        }
    }
}