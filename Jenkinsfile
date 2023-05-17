pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out the source code from the repository
                git 'git@github.com:deepu2899/python.git'
            }
        }

        stage('Build frontend') {
            steps {
                // Build the React frontend
                 def workspacePath = pwd(var/lib/jenkins/workspace)
                    def projectDirectory = "${var/lib/jenkins/workspace}/Deepak_sharma_master"
                    dir(projectDirectory) {frontend
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Build backend') {
            steps {
                // Build the Python backend
                sh 'pip install -r requirements.txt'
                // Additional build steps if required
            }
        }

        stage('Deploy') {
            steps {
                // Copy files to the server
                sh 'rsync -avz --delete frontend/ ssh root@165.22.66.188:/var/www/frontend/'
                sh 'rsync -avz --delete backend/ ssh root@165.22.66.188/var/www/backend/'
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
