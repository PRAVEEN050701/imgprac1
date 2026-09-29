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

                "C:\\Program Files\\Git\\cmd\\git.exe" remote remove target 2>NUL
                "C:\\Program Files\\Git\\cmd\\git.exe" remote add target https://github.com/PRAVEEN050701/imgprac2.git

                set "GIT_TERMINAL_PROMPT=0"
                set "GIT_ASKPASS=%WORKSPACE%\\askpass.bat"

                echo @echo off > "%GIT_ASKPASS%"
                echo if "%%1"=="Username for 'https://github.com/':" echo %%GIT_USERNAME%% >> "%GIT_ASKPASS%"
                echo if "%%1"=="Password for 'https://%%GIT_USERNAME%%@github.com/':" echo %%GIT_PASSWORD%% >> "%GIT_ASKPASS%"

                "C:\\Program Files\\Git\\cmd\\git.exe" push target HEAD:main
            '''
            )
        }
    }
}