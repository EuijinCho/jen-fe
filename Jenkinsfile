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
            	sh "aws s3 sync ./build s3://jen-fe --delete --profile default"
            	sh 'aws cloudfront create-invalidation --distribution-id E16N16FQO7NFSF --paths "/*"'
            }
        }
    }
}