pipeline{
    
    agent any
    environment{
        DOCKER_USERNAME="erpuser"
        APP_NAME = "gitops-argo-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTRY_CRED = 'dockerhub'
    }

        stages{

            stage('Clean WorkSpace'){

                    steps{

                        script {

                            cleanWs()
                        }
                    }
                }
            
            stage('Check SCM'){

                    steps{

                        script {

                            git credentialsId: 'github'
                            url: 'https://github.com/emushene/gitops_argocd_ci.git'
                            branch: 'master'
                        }
                    }
                }
           
            stage('Build Docker Image'){

                    steps{

                        script {
                            
                            docker_image= docker.build "${IMAGE_NAME}"
                            
                        }
                    }
                }
                 stage('Push Docker Image'){

                    steps{

                        script {
                            
                            docker.withRegistry('', REGISTRY_CRED){
                                docker_image.push("$BUILD_NUMBER")
                                docker_image.push('latest')
                            }
                            
                        }
                    }
                }

        }
}