pipeline {
    agent any
    environment {
        remoteHost = 'ubuntu@172.31.36.172'
        sshKeyPath = '/var/lib/jenkins/akash.pem'
    }
    stages {
        stage('Cleanup') {
            steps {
                sh "ssh -i ${sshKeyPath} ${remoteHost} 'docker stop my-html-app; docker rm my-html-app; docker rmi my-html-app; rm -rf SimpleWebsiteProject'"
            }
        }
        stage('Deploy') {
            steps {
                sh "ssh -i ${sshKeyPath} ${remoteHost} 'git clone https://github.com/akashbkochure/SimpleWebsiteProject.git; cd SimpleWebsiteProject; docker build -t my-html-app .; docker run -d -p 8080:80 --name my-html-app my-html-app'"
            }
        }
    }
}
