pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                sh 'sudo docker stop my-html-app || true' // Stop existing container
                sh 'sudo docker rm my-html-app || true'   // Remove existing container
                sh 'sudo docker rmi my-html-app || true'  // Remove existing image
                sh 'sudo rm -rf SimpleWebsiteProject'
                
            }
        }

        stage('Clone, Build and Deploy') {
            steps {
                sh 'sudo git clone https://github.com/akashbkochure/SimpleWebsiteProject.git'
                cd SimpleWebsiteProject
                sh 'docker build -t my-html-app .'
                sh 'docker run -d -p 8080:80 --name my-html-app my-html-app'
            }
        }
    }
}
