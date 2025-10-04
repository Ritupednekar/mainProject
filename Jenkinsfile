pipeline {
    agent none

    stages {
        stage('Deploy to Test') {
            when {
                branch 'develop'
            }
            agent {
                label 'Push-to-test'
            }
            steps {
                echo "Deploying to Test server..."
                // Assume you have an SSH credential set up in Jenkins with a private key
                // If you haven't, you need to create it in Manage Jenkins > Manage Credentials
                sshagent(credentials: ['Push-to-test']) {
                    sh "scp -r * ec2-user@34.207.242.97:"/home/ec2-user/workspace"
                }
            }
        }

        stage('Deploy to Prod') {
            when {
                branch 'develop'
            }
            agent {
                label 'Push-to-prod'
            }
            steps {
                echo "Deploying to Prod server..."
                sshagent(credentials: ['Push-to-prod']) {
                    sh "scp -r * ec2-user@54.243.26.166:"/home/ec2-user/workspace"
                }
            }
        }
    }
}
