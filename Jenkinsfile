pipeline{
    agent any
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t  node.js-demo:latest"
                echo "INFO:docker image built."
            }
        }
        stage('Docker image Deploy')
        {
            steps
            {
                echo "running the docker image."
                sh "docker rm -f node.js-demo || true"
                sh "docker run --restart always -p 3000:3000 -d --name nodejs-demo nodejs-demo:latest"
            }
        }
        stage('Deploy to k8's){
            steps{
                sshagent(['kops-machine']){
                    sh "service.yml nodeapp.yml ec2-user@18.236.99.72:/home/"
                    sh "ssh ec2-user@18.236.99.72 kubectl apply -f ."
                    sh "ssh ec2-user@18.236.99.72 kubectl create -f ."
                }
            }
        }
    }
}
