pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Push to imgprac2') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'github-credetials',
                        usernameVariable: 'GIT_USERNAME',
                        passwordVariable: 'GIT_PASSWORD'
                    )
                ]) {
                    bat '''
                        git config user.name "%GIT_USERNAME%"
                        git config user.email "praveenjb01@gmail.com"

                        git remote add target https://github.com/PRAVEEN050701/imgprac2.git
                        git push target HEAD:main
                    '''
                }
            }
        }
    }

    post {

        success {
            mail(
                to: 'praveenjb01@gmail.com',
                subject: "Build ${BUILD_NUMBER} - SUCCESS",
                body: "Build ${BUILD_NUMBER} completed successfully. Code was pushed from prac3 to prac4."
            )
        }

        failure {
            mail(
                to: 'praveenjb01@gmail.com',
                subject: "Build ${BUILD_NUMBER} - FAILURE",
                body: "Build ${BUILD_NUMBER} failed."
            )
        }
    }
}