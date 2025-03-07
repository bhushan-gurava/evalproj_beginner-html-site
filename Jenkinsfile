pipeline {
    agent { 
	label 'Build-Agent'
    }
    environment {
        DOCKERHUB_CREDENTIALS=credentials('e12f5850-04d6-469c-85e1-3a9fa3431c50')
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
		sh 'sudo docker build /home/ubuntu/jenkins/workspace/EvalProj-CI -t bhushang300912/image03072025'
		sh 'sudo docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW'
		sh 'sudo docker push bhushang300912/image03072025'
            }
        }
        stage('Kubernetes') {
            steps {
                sh 'kubectl apply /home/ubuntu/jenkins/workspace/Build/deploy.yaml'
                sh 'kubectl apply /home/ubuntu/jenkins/workspace/Build/service.yaml'
            }
        }
        stage('Finish') {
            steps {
                echo "Build ${env.BUILD_ID} is successful on ${env.JENKINS_URL}"
            }
        }
    }
}
