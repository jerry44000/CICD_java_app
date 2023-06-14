@Library('my-shared-library') _

pipeline{
    agent any

    parameters {
        choice(name: 'action', choices:'create\ndelete', description: 'Choose create/destroy')
        string(name: 'ImageName', description: 'name of the docker build', defaultValue: 'javapp')
        string(name: 'ImageTag', description: 'Tag of the docker build', defaultValue: 'v1')
        string(name: 'DockerHubUser', description: 'name of App', defaultValue: 'shaykube')
    }

    stages {

        stage('Git Checkout'){

        when { expression { params.action == 'create'} }

            steps{
                    gitCheckout(
                        branch: "main",
                        url: "https://github.com/jerry44000/CICD_java_app.git"
                    )             
            }
            
        }
        stage('Unit Test Maven'){

        when { expression { params.action == 'create'} }

                steps {
                    script {
                        mvnTest()
                    }
                }
            }
        stage('Integration Test Maven'){

        when { expression { params.action == 'create'} }

                steps {
                    script {
                        mavenIntegration()
                    }
                }
            }
        stage('Sonarqube Static Code Analysis'){

        when { expression { params.action == 'create'} }

               steps {
                  script {
                    def SonarQubecredentialsId = 'sonarqube-api'
                    staticCodeAnalysis(SonarQubecredentialsId)
                  }
               }  
        }
        stage('Sonarqube Quality Gate Status'){

        when { expression { params.action == 'create'} }

               steps {
                  script {
                    def SonarQubecredentialsId = 'sonarqube-api'
                    qualityGateStatus(SonarQubecredentialsId)
                  }
               }  
        }
        stage('Maven Build'){

        when { expression { params.action == 'create'} }

               steps {
                  script {
                    mvnBuild()
                  }
               }  
        }
        stage('Docker Image Build'){

        when { expression { params.action == 'create'} }

               steps {
                  script {
                    dockerBuild("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
                  }
               }  
        }
        stage('Trivy Docker Image Scan'){

        when { expression { params.action == 'create'} }

               steps {
                  script {
                    dockerImageScan("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
                  }
               }  
        }
        stage('Push Docker Image on DockerHub'){

        when { expression { params.action == 'create'} }

               steps {
                  script {
                    dockerImagePush("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
                  }
               }  
        }
    }
}

