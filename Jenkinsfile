pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        STACK_NAME = 'my-cloudformation-stack'
        TEMPLATE_FILE = 'cloudformation/my-stack-template.yaml'
        PARAMETERS_FILE = 'cloudformation/parameters.json'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Muthu-git10/Demorep.git',
                    credentialsId: 'Gitcredential'
            }
        }

        stage('Deploy CloudFormation Stack') {
            steps {
                withAWS(credentials: 'aws-jenkins-creds', region: "${AWS_DEFAULT_REGION}") {
                    bat """
                    aws cloudformation deploy ^
                        --stack-name ${STACK_NAME} ^
                        --template-file ${TEMPLATE_FILE} ^
                        --parameter-overrides file://${PARAMETERS_FILE} ^
                        --capabilities CAPABILITY_NAMED_IAM
                    """
                }
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed.'
        }
    }
}
