pipeline {
    agent none
    parameters {
        choice(name: 'ENVIRONMENT',
            choices: ['DEVELOPMENT' , 'STAGING', 'PRODUCTION'],
            description: 'Choose the environment for this deployment')
    }
    stages {
        stage ('Build') {
            steps {
                echo "Building the job."
            }
        }
        stage ('Deploy to the non-production environments.') {
            when {
                // Only deploy if the environment is NOT production
                expression { params.ENVIRONMENT != 'PRODUCTION' }
            }
            steps {
                echo "Deploying to ${params.ENVIRONMENT}"
            }
        }
        stage ('Deploy to the Production environment.') {
            agent none
            when {
                expression { params.ENVIRONMENT == 'PRODUCTION' }
            }
            steps {
                input message: 'Confirm deployment to the production environment?', ok: 'Deploy'
                echo "Deploying to ${params.ENVIRONMENT}"
            }
        }
    }
}
