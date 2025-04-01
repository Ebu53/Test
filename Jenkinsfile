pipeline {

    agent { label 'MacOs' }


    environment {

        GITHUB_REPO = "picarro/pcubed-mobile.git"

        GITHUB_TOKEN = credentials('bitkraft-github-token')

    }
 
    triggers {

         pollSCM('H/10 * * * *')

     }


    stages {

        stage('Checkout Code') {

            steps {

                script {

                    def selectedBranch = 'develop'

                    withCredentials([string(credentialsId: 'bitkraft-github-token', variable: 'TOKEN')]) {

                        sh "git config --global credential.helper store"

                        def repoUrl = "https://${TOKEN}@github.com/${GITHUB_REPO}"

                        // sh "git clone ${repoUrl} ."

                        sh "git checkout ${selectedBranch}"

                    }

                }

            }

        }


        stage('Install Dependencies') {

            steps {

                script {

                   sh 'test'

                }

            }

        }



    } 

    post {

        always {

            script {

                // Clean up based on environment

                sh """

                    rm -f .netrc

                    rm -f android/app/my-upload-key.keystore

                    if [ "${params.ENVIRONMENT}" = "dev" ]; then

                        rm -f .env.development

                    else

                        rm -f .env.staging

                    fi

                    echo "Workspace cleaned up successfully"

                """

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
 
