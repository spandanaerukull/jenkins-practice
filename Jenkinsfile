# This is a Jenkins pipeline script that defines a CI/CD pipeline for a project. The pipeline is configured to run on an agent labeled 'AGENT-1' and has several stages: Build, Test, and Deploy. It also includes environment variables, options for timeout and concurrent builds, and parameters for user input. The Deploy stage includes an input step that requires user confirmation before proceeding. Finally, the post section defines actions to take after the pipeline execution, such as always deleting the workspace directory and printing messages based on the success or failure of the build.
pipeline { # Define a Jenkins pipeline
    agent  {
        label 'AGENT-1'
    }
    environment { 
        COURSE = 'jenkins'
    }
    options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password') 
    }
    // Build
    stages {
        stage('Build') {
            steps {
                script{
                    sh """
                        echo "Hello Build"
                        sleep 10
                        env
                        echo "Hello ${params.PERSON}"
                    """
                }
            }
        }
        stage('Test') {
            steps {
                script{
                    echo 'Testing..'
                }
            }
        }
        stage('Deploy') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
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
            deleteDir()
        }
        success { 
            echo 'Hello Success'
        }
        failure { 
            echo 'Hello Failure'
        }
    }
}