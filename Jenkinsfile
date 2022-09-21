pipeline{
    agent any
    environment{DOCKER_TAG = getDockerTag()
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
    }
}
