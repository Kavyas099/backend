pipeline {
    agent { label 'kavya' }

    environment { 
        PROJECT = 'expense'
        COMPONENT = 'backend'
        appVersion = ''
        ACC_ID = '315069654700'
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 30, unit: 'MINUTES')
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Debug JSON File') {
            steps {
                sh 'pwd'
                sh 'ls -l'
                sh 'cat package.json || echo "package.json not found"'
            }
        }

        stage('Read Version') {
            steps {
                script {
                    def content = readFile('package.json')
                    def packageJson = new groovy.json.JsonSlurper().parseText(content)
                    echo "Version is: ${packageJson.version}"

                }
            }
        }

        stage ( 'install depends') {
            steps {
                script {
                    sh '''
                    npm install
                    '''
                }
            }
        }

        stage ( 'build image'){
            steps{
                script {
                    sh '''
                    docker build -t backend:1.0.0 .
                    '''
                    }
                }
            }
        
    }

    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        failure { 
            echo 'I will run when pipeline is failed'
        }
        success { 
            echo 'I will run when pipeline is success'
        }
    }
}
