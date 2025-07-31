pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        STACK_NAME = 'my-cloudformation-stack'
        TEMPLATE_FILE = 'cloudformation/my-stack-template.yaml'
        PARAMETERS = 'KeyName=forvpcppk InstanceType=t3.micro'	
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
                withAWS(credentials: 'AKIA3DQM53PU5UEPCL6O', region: "${AWS_DEFAULT_REGION}") {
                    bat """
                        aws cloudformation deploy ^
                            --stack-name ${STACK_NAME} ^
                            --template-file ${TEMPLATE_FILE} ^
                            --parameter-overrides ${PARAMETERS} ^
                            --capabilities CAPABILITY_NAMED_IAM
                    """
                }
            }
        }

		stage('Fetch Stack Outputs') {
			steps {
				withAWS(credentials: 'AKIA3DQM53PU5UEPCL6O', region: "${AWS_DEFAULT_REGION}") {
					script {
						def output = bat (
							script: """
								aws cloudformation describe-stacks ^
									--stack-name ${STACK_NAME} ^
									--query "Stacks[0].Outputs" ^
									--output text
							""",
							returnStdout: true
						).trim()
						echo "📦 Stack Outputs:\n${output}"
					}
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