pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'  // Change to your desired AWS region
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
				withAWS(credentials: 'AKIA3DQM53PU5UEPCL6O', region: 'us-east-1') {
					bat """
						aws cloudformation deploy ^
							--stack-name my-cloudformation-stack ^
							--template-file cloudformation/my-stack-template.yaml ^
							--parameter-overrides file://cloudformation/parameters.json ^
							--capabilities CAPABILITY_NAMED_IAM
					"""
				}
			}
		}

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
