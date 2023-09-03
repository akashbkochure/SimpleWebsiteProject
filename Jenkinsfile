pipeline {
    agent any

    stages {
/*        stage('Cleanup') {
            steps {
                script {
                    def remoteHost = 'ubuntu@172.31.36.172'
                    def sshKeyPath = '/var/lib/jenkins/akash.pem'
                    
                    sh """
                    sudo ssh -i ${sshKeyPath} -o StrictHostKeyChecking=no ${remoteHost} << 'EOF'
                    sudo docker stop my-html-app 
                    sudo docker rm my-html-app 
                    sudo docker rmi my-html-app 
                    sudo rm -rf SimpleWebsiteProject
                    EOF
                    """
                }
            }
        }*/

        stage('Clone, Build and Deploy') {
            steps {
                script {
                    def remoteHost = 'ubuntu@172.31.36.172'
                    def sshKeyPath = '/var/lib/jenkins/akash.pem'
                    
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
