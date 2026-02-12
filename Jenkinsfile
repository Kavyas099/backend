pipeline {
    agent { label 'kavya' }

    environment {
        PROJECT = 'expense'
        ENVIRONMENT = 'Dev'
        APP_VERSION = ''
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 30, unit: 'MINUTES')
    }

    stages {
        stage('Read Version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package copy.json'
                    APP_VERSION = packageJson.version
                    echo "App version is ${APP_VERSION}"
                }
            }
        }
    }

    post {
        always {
            echo "I will say again hello"
        }

        success {
            echo "I will say for success"
        }

        failure {
            echo "I will say for failure"
        }
    }
}
