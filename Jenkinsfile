pipeline {
    agent { label 'kavya' }

    environment { 
        PROJECT = 'expense'
        COMPONENT = 'backend'
        appVersion = ''
        ACC_ID = '130954245108'
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

        stage('Read Version') {
            steps {
                script {
                    def content = readFile('package.json')
                    def packageJson = new groovy.json.JsonSlurper().parseText(content)
                    env.appVersion = packageJson.version
                    echo "Version is: ${env.appVersion}"
                }
            }
        }

        stage('Install Depends') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build & Push Image') {
            steps {
                script {
                    withAWS(region: 'us-east-1', credentials: 'awscreds') {
                        sh """
                        aws ecr get-login-password --region us-east-1 | \
                        docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com

                        docker build -t ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}/${COMPONENT}:${env.appVersion} .

                        docker push ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${PROJECT}/${COMPONENT}:${env.appVersion}
                        """
                    }
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
