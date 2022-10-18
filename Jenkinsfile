pipeline {
    agent { label 'docker_agents' }


    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                //git 'git@github.com:Mo7amed-3laa2/jenkins_nodejs_example.git'

                // build simple-app then run it as a container
                sh "docker build --tag mohamedalaa98/simple-app-node:latest ."
                sh "docker run -p 3000:3000 --name simple-app mohamedalaa98/simple-app-node:latest"
            }

        }
    }
}
