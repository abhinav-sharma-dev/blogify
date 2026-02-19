pipeline {
    agent any

    environment {
        EC2_HOST = '13.126.242.111'
        PROJECT_DIR = '/home/ubuntu/blogify'
    }

    stages {

        stage('Deploy Backend to EC2') {
            steps {
                sshagent(['ec2-key']) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ubuntu@${EC2_HOST} '
                            cd ${PROJECT_DIR} &&
                            git pull origin main &&
                            npm install &&
                            pm2 restart blogify || pm2 start app.js --name blogify
                        '
                    """
                }
            }
        }
    }
}
