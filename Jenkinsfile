pipeline {
    agent  {
        label 'agent1'
    }
    environment { 
        appVersion = ""
        appName = ""    
    }
    options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds() //it will used for not trigger and run pipelines the same pipeline at same time.
    }
    
    // Build
    stages {
        stage('Read Package JSON') {
            steps {
                script {
                    // 1. Read the package.json file from the workspace
                    def packageJson = readJSON file: 'package.json'
                    
                    // 2. Extract values into variables
                    def appName = packageJson.name
                    def appVersion = packageJson.version
                    
                    // 3. Print the values to the build logs
                    echo "Application Name: ${appName}"
                    echo "Application Version: ${appVersion}"
                    
                    
                }
            }

        }
        
        stage('Install Dependencies') {
            steps {
                script{
                    sh """
                        npm install
                    """
                }
            }
        }
        stage('Deploy') {
           /*  input {  //these are used for taking the approval or input from the user
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            } */
            steps {
                script{
                    echo "Hello, ${PERSON}, nice to meet you."
                    echo 'Deploying..'
                }
            }
        }
        
    }

    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir() //it will delete the directory once build success.
        }
        success { 
            echo 'Hello Success'
        }
        failure { 
            echo 'Hello Failure'
        }
    }
}