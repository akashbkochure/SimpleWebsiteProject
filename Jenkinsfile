pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                script {
                    def remoteHost = 'ubuntu@172.31.36.172'
                    def sshKeyPath = '/var/lib/jenkins/akash.pem'

                    // Check if the container exists before stopping and removing it
                    def containerExists = sh(script: "sudo ssh -i ${sshKeyPath} -o StrictHostKeyChecking=no ${remoteHost} 'sudo docker ps -a | grep my-html-app'", returnStatus: true)
                    if (containerExists == 0) {
                        sh """
                        sudo ssh -i ${sshKeyPath} -o StrictHostKeyChecking=no ${remoteHost} << 'EOF'
                        sudo docker stop my-html-app
                        sudo docker rm my-html-app
                        sudo docker rmi my-html-app
                        sudo rm -rf SimpleWebsiteProject
EOF
                        """
                    } else {
                        echo "Container 'my-html-app' not found, nothing to clean up."
                    }
                }
            }
        }

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
