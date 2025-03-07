pipeline {
    agent{ 
	label 'EvalFinalProj-Agent'
    }
    environment {
        DOCKERHUB_CREDENTIALS=credentials('36c3d51d-cb2a-4eb5-8853-42f0ebb1a1f0')
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
		sh 'sudo docker build /home/ubuntu/jenkins/workspace/Build -t bhushang300912/image03072025'
		sh 'sudo docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW'
		sh 'sudo docker push bhushang300912/image03072025'
            }
        }
        stage('Kubernetes') {
            steps {
                sh 'kubectl create -f ./deploy.yml'
                sh 'kubectl create -f ./service.yml'
            }
        }
        stage('Finish') {
            steps {
                echo "Build ${env.BUILD_ID} is successful on ${env.JENKINS_URL}"
            }
        }
    }
}
