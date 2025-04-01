pipeline {

    agent { label 'MacOs' }


    environment {

        GITHUB_REPO = "Ebu53/Test"
    }
 
    triggers {

         pollSCM('H/10 * * * *')

     }


    stages {

        stage('Checkout Code') {

            steps {

                script {

                        def selectedBranch = 'dev'
                        sh "git config --global credential.helper store"
                        def repoUrl = "https://${TOKEN}@github.com/${GITHUB_REPO}"
                        sh "git clone ${repoUrl} ."
                        sh "git checkout ${selectedBranch}"

                }

            }

        }


        stage('Install Dependencies') {

            steps {

                script {

                   sh 'ls'

                }

            }

        }



    } 

    post {

        always {

            script {

                // Clean up based on environment

                deleteDir()

            }

        }

        success {

            echo 'Build and Deployment Successful!'

        }

        failure {

            echo 'Build or Deployment Failed!'

        }

    }

}
 
