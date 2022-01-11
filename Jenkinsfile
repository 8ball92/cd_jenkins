pipeline {
    agent any
    environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
        
	}
    stages {
        stage('Pull Image') {  
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh "docker pull gblbjj/${env.APP}:${env.TAG_VERSION}"   
            }
        }
        stage('Deploy') {
            // when { expression { return env.BRANCH == 'develop'} }
            steps {
                git branch: "${env.BRANCH}",
                    url: 'https://github.com/8ball92/ci_cd-stack.git'
            
               
                   
            }        
                     
        }
    }
    post {
        always {
            script {
                echo "THE END JOB"
                sh "docker rmi gblbjj/${env.APP}:${env.TAG_VERSION}"
                
            }
            
            cleanWs deleteDirs: true, patterns: [[pattern: '', type: 'EXCLUDE']]
        }
    }        
}
