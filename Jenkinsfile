pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                script {
                    sh """
                    ssh -i /home/ubuntu/akash.pem -o StrictHostKeyChecking=no ubuntu@54.221.175.144 << 'EOF'
                    docker stop my-html-app || true
                    docker rm my-html-app || true
                    docker rmi my-html-app || true
                    rm -rf SimpleWebsiteProject
                    EOF
                    """
                }
            }
        }

        stage('Clone, Build and Deploy') {
            steps {
                script {
                    sh """
                    ssh -i /home/ubuntu/akash.pem -o StrictHostKeyChecking=no ubuntu@54.221.175.144 << 'EOF'
                    git clone https://github.com/akashbkochure/SimpleWebsiteProject.git
                    cd SimpleWebsiteProject
                    docker build -t my-html-app .
                    docker run -d -p 8080:80 --name my-html-app my-html-app
                    EOF
                    """
                }
            }
        }
    }
}
