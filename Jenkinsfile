pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        STACK_NAME = 'ec2-tomcat-stack'
        TEMPLATE_FILE = 'cloudformation/ec2-tomcat.yaml
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

        stage('Deploy EC2 with Tomcat') {
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

        stage('Show Stack Outputs') {
            steps {
                withAWS(credentials: 'AKIA3DQM53PU5UEPCL6O', region: "${AWS_DEFAULT_REGION}") {
                    script {
                        def output = bat (
                            script: """
                            aws cloudformation describe-stacks ^
                                --stack-name ${STACK_NAME} ^
                                --query "Stacks[0].Outputs" ^
                                --output table
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
            echo '✅ Tomcat EC2 instance deployed successfully!'
        }
        failure {
            echo '❌ Deployment failed.'
        }
    }
}
