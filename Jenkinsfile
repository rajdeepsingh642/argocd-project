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
            
    }
}