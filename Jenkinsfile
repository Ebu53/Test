pipeline {

    agent { label 'built-in' }


    environment {

        GITHUB_REPO = "Ebu53/Test"
        TOKEN = "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"
    }
 
    triggers {
        pollSCM('* * * * *')
     }


    stages {

        stage('Checkout Code') {

            steps {

                script {
                        echo 'Hello, Jenkins!'
                        def selectedBranch = 'stage'
                        sh "git config --global credential.helper store"
                        def repoUrl = "https://${TOKEN}@github.com/${GITHUB_REPO}"
                        sh "git clone ${repoUrl} ."
                        sh "git checkout ${selectedBranch}"

                }

            }

        }



    } 

    post {

        success {

            echo 'Build and Deployment Successful!'

        }

        failure {

            echo 'Build or Deployment Failed!'

        }

    }

}
 
