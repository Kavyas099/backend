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
                def packageJson = readJSON file: 'package.json'
                echo "Version is: ${packageJson.version}"
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