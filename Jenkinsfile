pipeline {
	agent{ 
		label 'EvalFinalProj-Agent'
	}
	
    environment {
        DOCKERHUB_CREDENTIALS=credentials('4e3d30b0-0ae5-46df-9361-6b450c6db8c6')
    }
	
    stages {
        stage('Start') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            }
        }
        stage('Git'){
            steps{
                git'https://github.com/bhushan-gurava/evalproj_beginner-html-site.git'
            }
        }
        stage('Docker') {
            steps {
                sh 'sudo docker build /home/ubuntu/jenkins/workspace/Build -t docker6161/image'
                sh 'sudo echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'sudo docker push docker6161/image'
            }
        }
        stage('Kubernetes') {
            steps {
                sh 'kubectl create -f deploy.yml'
                sh 'kubectl create -f service.yml'
            }
        }
        stage('Finish') {
            steps {
                echo "Build ${env.BUILD_ID} is successful on ${env.JENKINS_URL}"
            }
        }
    }
}
