pipeline {
    agent any

    environment {
        EC2_HOST = '15.207.106.46'
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
                            pm2 describe blogify > /dev/null 2>&1 &&
                            pm2 restart blogify ||
                            pm2 start app.js --name blogify --watch -- --port 8000
                        '
                    """
                }
            }
        }
    }
}
