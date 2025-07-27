pipeline {
    agent any  // Use any available Jenkins agent

    environment {
        GIT_REPO = 'git@github.com:your-username/your-repo.git'  // <-- Update this!
        BRANCH = 'main'  // Change if you use a different branch
    }

    stages {
     
		stage('Build') {
            steps {
                echo 'Building the project...'
                // Example: sh 'mvn clean install'  // For Maven Java projects
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Example: sh 'npm test'  // For Node.js projects
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
