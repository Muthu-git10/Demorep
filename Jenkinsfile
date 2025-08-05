pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        STACK_NAME = 'New stack for Jenkinscreation'
        TEMPLATE_FILE = 'cloudformation/my-stack-template.yaml'
        PARAMETERS = 'KeyName=forvpcppk InstanceType=t3.small'	
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
                    bat """
                        aws cloudformation deploy ^
                            --stack-name ${STACK_NAME} ^
                            --template-file ${TEMPLATE_FILE} ^
                            --parameter-overrides ${PARAMETERS} ^
<<<<<<< HEAD
                            --capabilities CAPABILITY_NAMED_IAM ^
							--region us-east-1
                    """
            }
=======
                            --capabilities CAPABILITY_NAMED_IAM --region ${AWS_DEFAULT_REGION} ^
                            --no-fail-on-empty-changeset
                    """
                }
>>>>>>> ab19bddfd64cbda513e472f515824668f4c27c5e
        }

		stage('Fetch Stack Outputs') {
			steps {
					script {
						def output = bat (
							script: """
								aws cloudformation describe-stacks ^
									--stack-name ${STACK_NAME} ^
									--query "Stacks[0].Outputs" ^
<<<<<<< HEAD
									--output text ^
									--region us-east-1
=======
									--output text --region ${AWS_DEFAULT_REGION}
>>>>>>> ab19bddfd64cbda513e472f515824668f4c27c5e
							""",
							returnStdout: true
						).trim()
						echo "📦 Stack Outputs:\n${output}"
					}
<<<<<<< HEAD
				}
=======
			}
>>>>>>> ab19bddfd64cbda513e472f515824668f4c27c5e
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