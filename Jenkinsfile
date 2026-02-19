pipeline {
    agent any

    environment {
        EC2_HOST = 'ubuntu@13.126.242.111'
        PROJECT_DIR = '/home/ubuntu/blogify'
    }

    stages {

        stage('Deploy Backend to EC2') {
            steps {
                sh """
                ssh -o StrictHostKeyChecking=no ${EC2_HOST} << 'EOF'
                    cd ${PROJECT_DIR}
                    git pull origin main
                    npm install
                    pm2 restart blogify || pm2 start app.js --name blogify
                EOF
                """
            }
        }
    }
}
