
pipeline {
    AGENT = { label 'kavya'} {


        environment {
            PROJECT = 'expense'
            ENVIRONMENT = 'Dev'
            APP_VERSION = ''
        }
        options {
            disableConcurrentBuilds ()
            timeout (time: 30, unit: 'MINUTES')
        }
        
        stages {
            stage {
                steps {
                    script {
                    def packageJson = readJSON file: 'package.json'
                    APP_VERSION = packageJson.version
                    echo "appversion is $APP_VERSION"
                    }
                }
          
          
            }
            
        }

        
    }

    post {
        always  {
            echo "i will say again hello "
        }


        success {
        echo "I will say for sucess"
        }
    

        failure {
        echo "i willsay for failure"
    }

    }
}


