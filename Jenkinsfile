pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out the source code from the repository
                git 'git@github.com:deepu2899/python.git'
            }
        }
        stage('Build backend') {
            steps {
                // Build the Python backend
               sh 'cd backend && pip install -r requirements.txt'
                sh '$ openssl rand 256 > secret.key'
                  sh 'cd frontend && npm install && npm run build'
            }
        }

        stage('Deploy') {
            steps {
                // Copy files to the server
               //sh 'rsync -avz --delete frontend/ ssh root@165.22.66.188:/var/www/frontend/'
              sh 'rsync -avz --delete /var/lib/jenkins/workspace/Deepak_sharma_master/ ssh root@165.22.66.188:/var/www/backend/'

            }
        }

        stage('Restart server') {
            steps {
                // Restart the server or necessary services
                sh 'ssh root@165.22.66.188 "sudo systemctl restart backend"'
            }
        }
    }
}
