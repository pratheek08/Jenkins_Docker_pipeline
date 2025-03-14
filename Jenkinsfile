pipeline{
	agent any
	environment{
		DOCKER_IMAGE = "pratheek008/my-jenkins-app"
		DOCKER_CREDENTIALS_ID = "39267e43-9788-4c04-9501-114511bd964d"

	}
	stages {
        stage('Clone Repository') {
            steps {
                echo "Cloning repository..."
                git url: 'https://github.com/pratheek08/Jenkins_Docker_pipeline.git', branch: 'main'
                echo "Repository cloned successfully."
            }
        }
	stage('Docker Login') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        echo "Logged into Docker Hub"
                    }
                }
            }
        }

        stage('Build Docker Image') {
    steps {
        script {
            echo "Logging into Docker Hub..."
                docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
            echo "Docker image built successfully."
        }
    }
}


	stage('Run Container Locally'){
		steps {
			script {
				sh "docker run -d -p 8050:80 --name jenkins-docker ${DOCKER_IMAGE}:latest"
			}
		}
}

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        echo "Pushing Docker image..."
                        sh "docker push ${DOCKER_IMAGE}"
                        echo "Docker image pushed successfully."
                    }
                }
            }

        }
        stage('Deploy to server') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {

			sh "docker pull pratheek008/my-jenkins-app:latest"

}

                }
            }
        }

    }
}
