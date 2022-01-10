pipeline {
    agent any
    environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
        GitHubUser = credentials('github')
	}
    stages {
        stage('Pull Image') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh "docker pull gblbjj/${env.APP}:${env.TAG_VERSION}"   
            }
        }
        stage('Deploy') {
            steps {
                sh "git clone http://$GitHubUser_USR:$GitHubUser_PSW@https://github.com/8ball92/deploy_hello_world.git"
                 
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
