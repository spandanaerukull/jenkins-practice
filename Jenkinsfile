// This is a Jenkins pipeline script that defines a CI/CD pipeline for a project. The pipeline is configured to run on an agent labeled 'AGENT-1' and has several stages: Build, Test, and Deploy. It also includes environment variables, options for timeout and concurrent builds, and parameters for user input. The Deploy stage includes an input step that requires user confirmation before proceeding. Finally, the post section defines actions to take after the pipeline execution, such as always deleting the workspace directory and printing messages based on the success or failure of the build.
pipeline { // Define a Jenkins pipeline
    agent  {
        label 'AGENT-1'
    }
    environment { 
        COURSE = 'jenkins'
    }
    options { // Define options for the pipeline, these options include setting a timeout for the pipeline execution to prevent it from running indefinitely and disabling concurrent builds to ensure that only one instance of the pipeline runs at a time, which can help avoid conflicts and resource contention.
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
    }
    parameters { // Define parameters for user input when triggering the pipeline, these parameters allow users to provide input values that can be used in the pipeline execution, such as specifying a person's name, providing a biography, toggling a boolean value, making a choice from a list of options, or entering a password. These parameters can be accessed in the pipeline using the `params` object, for example `params.PERSON` to get the value of the PERSON parameter.
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
        always {  // this block will always execute regardless of the build result, it is used to perform cleanup actions or any necessary steps that should be executed after every build, in this case we are deleting the workspace directory to clean up any files or artifacts generated during the build process and also printing a message to indicate that this block has been executed.
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success {  // this block will execute only if the build is successful, it is used to perform actions that should only be executed when the build succeeds, in this case we are printing a message to indicate that the build was successful.
            echo 'Hello Success'
        }
        failure { // this block will execute only if the build fails, it is used to perform actions that should only be executed when the build fails, in this case we are printing a message to indicate that the build has failed.
            echo 'Hello Failure'
        }
    }
}