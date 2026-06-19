pipeline {
    agent any

    environment {
        ANDROID_HOME = "/home/taranmeet/Android/Sdk"
        PATH = "${env.ANDROID_HOME}/tools:${env.ANDROID_HOME}/platform-tools:${env.PATH}"
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/Taranmeet/Ecommerce',
                    branch: 'main'
            }
        }

        stage('Lint') {
            steps {
                sh './gradlew lint'
            }
            post {
                always {
                    // Archives the lint report so you can view it in Jenkins UI
                    archiveArtifacts artifacts: '**/reports/lint-results*.html',
                                     allowEmptyArchive: true
                }
            }
        }

        stage('Build Debug APK') {
            steps {
                sh './gradlew assembleDebug'
            }
            post {
                success {
                    // Archives the APK so you can download it from Jenkins UI
                    archiveArtifacts artifacts: '**/outputs/apk/debug/*.apk',
                                     allowEmptyArchive: true
                }
            }
        }

    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed — check the logs above.'
        }
    }
}
