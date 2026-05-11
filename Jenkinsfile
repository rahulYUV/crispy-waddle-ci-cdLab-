pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'test -f index.html'
                        sh 'test -f app.js'
                    } else {
                        bat 'if not exist index.html exit /b 1'
                        bat 'if not exist app.js exit /b 1'
                    }
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'rm -rf dist && mkdir -p dist && cp index.html app.js dist/'
                    } else {
                        bat 'if exist dist rmdir /s /q dist'
                        bat 'mkdir dist'
                        bat 'copy /y index.html dist\\'
                        bat 'copy /y app.js dist\\'
                    }
                }
                archiveArtifacts artifacts: 'dist/**', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def deployDir = env.DEPLOY_DIR?.trim()

                    if (deployDir) {
                        if (isUnix()) {
                            sh "rm -rf '${deployDir}' && mkdir -p '${deployDir}' && cp -r dist/* '${deployDir}/'"
                        } else {
                            powershell """
                                if (Test-Path '${deployDir}') {
                                    Remove-Item -Recurse -Force '${deployDir}'
                                }
                                New-Item -ItemType Directory -Force -Path '${deployDir}' | Out-Null
                                Copy-Item -Path 'dist\\*' -Destination '${deployDir}' -Recurse -Force
                            """
                        }
                    } else {
                        echo 'DEPLOY_DIR is not set, so deployment is limited to archived build output.'
                    }
                }
            }
        }
    }
}