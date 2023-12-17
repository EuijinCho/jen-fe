pipeline {
	agent any

    stages {
    	
        stage('Npm Build') {
        	steps {
                nodejs('NodeJS 18.7.0'){
                    sh "yarn install"
                    sh "yarn run build"
                }
            }
        }
        stage('Deploy') {
        	steps{
                withCredentials([<object of type com.cloudbees.jenkins.plugins.awscredentials.AmazonWebServicesCredentialsBinding>]) {
                    sh "aws s3 sync ./build s3://jen-fe"
            	    sh 'aws cloudfront create-invalidation --distribution-id E16N16FQO7NFSF --paths "/*"' 
                }
                // withCredentials([aws(credentialsId: 'tony.cho',accessKeyVariable: 'AWS_ACCESS_KEY_ID',secretKeyVariable:'AWS_SECRET_ACCESS_KEY')]) {
                //     sh "aws s3 sync ./build s3://jen-fe"
            	//     sh 'aws cloudfront create-invalidation --distribution-id E16N16FQO7NFSF --paths "/*"'     
                // }
            }
        }
    }
}