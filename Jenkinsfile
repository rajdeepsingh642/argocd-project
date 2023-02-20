pipeline {
    
	agent any

   
    stages{
        
        stage('Git checkout'){
            steps {
             git 'https://github.com/rajdeepsingh642/argocd-project.git'
            }
        }
        stage('Build docker image'){
            steps{
                sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID .'
                sh 'docker image tag $JOB_NAME:v1.$BUILD_ID rajdeepsingh642/$JOB_NAME:v1.$BUILD_ID'

                
            }
        }   
        stage('Pushing image to docker hub') {
            steps{
                withCredentials([string(credentialsId: 'rajdeepsingh642', variable: 'dockerhub')]) {
                sh "docker login -u rajdeepsingh642 -p ${dockerhub}"
                sh 'docker image push rajdeepsingh642/$JOB_NAME:v1.$BUILD_ID'
                 }
             }
        }
        stage('updating k8s deployment'){
            steps{
                sh """
                cat deployment.yml
                sed -i 's/${JOB_NAME}.*/${JOB_NAME}:${BUILD_ID}/g' deployment.yml
                cat deployment.yml
                """
            }
        } 
    }
}