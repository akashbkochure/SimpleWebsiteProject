pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                script {
                    // Execute cleanup steps on the remote server
                    sshagent(credentials: ['your-ssh-credentials-id']) {
                        sh """
                        ssh -i akash.pem -o StrictHostKeyChecking=no ubuntu@54.211.233.129 <<EOF
                        sudo docker stop my-html-app || true
                        sudo docker rm my-html-app || true
                        sudo docker rmi my-html-app || true
                        sudo rm -rf SimpleWebsiteProject
                        EOF
                        """
                    }
                }
            }
        }

        stage('Clone, Build and Deploy') {
            steps {
                script {
                    // Execute clone, build, and deploy steps on the remote server
                    sshagent(credentials: ['your-ssh-credentials-id']) {
                        sh """
                        ssh -i akash.pem -o StrictHostKeyChecking=no ubuntu@54.211.233.129 <<EOF
                        sudo git clone https://github.com/akashbkochure/SimpleWebsiteProject.git
                        cd SimpleWebsiteProject
                        sudo docker build -t my-html-app .
                        sudo docker run -d -p 8080:80 --name my-html-app my-html-app
                        EOF
                        """
                    }
                }
            }
        }
    }
}
