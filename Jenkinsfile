pipeline {
    agent { label 'instance_agents' }


    stages {
        stage('Build') {
            steps {
                echo "Get some code from a GitHub repository"
                echo "build simple-app docker file"
                sh "docker build --tag mohamedalaa98/simple-app-node:V1.${BUILD_ID} ."
            }

        }
        stage('Push') {
            steps {
                echo "push simple-app image to docker-hub"
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                sh "echo $PASS | docker login -u $USER --password-stdin"
                sh "docker push mohamedalaa98/simple-app-node:V1.${BUILD_ID}" 
                }
            }
            post {
                success {
                    slackSend color: "good", message: "github web-hook triggered! and build ${ BUILD_TAG } Succeeded !"
                }
                failure {
                    slackSend color: "danger", message: "github web-hook triggered! and build ${ BUILD_TAG } Failed !!!"
                }
            } 
        }
    }
}
