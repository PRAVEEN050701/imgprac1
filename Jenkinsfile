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
                "C:\\Program Files\\Git\\cmd\\git.exe" config user.name "%GIT_USERNAME%"
                "C:\\Program Files\\Git\\cmd\\git.exe" config user.email "praveenjb01@gmail.com"

                set "HOME=%WORKSPACE%"

                echo protocol=https> "%WORKSPACE%\\git-credential-input.txt"
                echo host=github.com>> "%WORKSPACE%\\git-credential-input.txt"
                echo username=%GIT_USERNAME%>> "%WORKSPACE%\\git-credential-input.txt"
                echo password=%GIT_PASSWORD%>> "%WORKSPACE%\\git-credential-input.txt"

                "C:\\Program Files\\Git\\cmd\\git.exe" credential approve < "%WORKSPACE%\\git-credential-input.txt"

                "C:\\Program Files\\Git\\cmd\\git.exe" remote remove target 2>NUL
                "C:\\Program Files\\Git\\cmd\\git.exe" remote add target https://github.com/PRAVEEN050701/imgprac2.git

                "C:\\Program Files\\Git\\cmd\\git.exe" push target HEAD:main

                del "%WORKSPACE%\\git-credential-input.txt"
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
                body: "Build ${BUILD_NUMBER} completed successfully. Code was pushed from imgprac1 to imgprac2."
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