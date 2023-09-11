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
                stage('Checkout SCM'){
                    steps{

                        step{
                            script{
                                git credentialsId: 'github',
                                url: 'https://github.com/emushene/gitops_argocd_ci.git',
                                branch: 'main'
                            }
                        }
                    }
                }

        }




}