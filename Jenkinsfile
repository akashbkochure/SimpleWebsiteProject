pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                script {
                    sudo cp /home/ubuntu/akash.pem /var/lib/jenkins/.ssh/akash.pem
                    sudo chown jenkins:jenkins /var/lib/jenkins/.ssh/akash.pem
                    sudo chmod 600 /var/lib/jenkins/.ssh/akash.pem

                    def remoteHost = 'ubuntu@54.221.175.144'
                    def sshKeyPath = '/var/lib/jenkins/.ssh/akash.pem'
                    
                    sh """
                    sudo ssh -i ${sshKeyPath} -o StrictHostKeyChecking=no ${remoteHost} << 'EOF'
                    sudo docker stop my-html-app || true
                    sudo docker rm my-html-app || true
                    sudo docker rmi my-html-app || true
                    sudo rm -rf SimpleWebsiteProject || true
                    EOF
                    """
                }
            }
        }

        stage('Clone, Build and Deploy') {
            steps {
                script {
                    def remoteHost = 'ubuntu@54.221.175.144'
                    def sshKeyPath = '/var/lib/jenkins/.ssh/akash.pem'
                    
                    sh """
                    sudo ssh -i ${sshKeyPath} -o StrictHostKeyChecking=no ${remoteHost} << 'EOF'
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
