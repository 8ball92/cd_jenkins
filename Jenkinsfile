pipeline {
    agent any
    environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
        
	}
    stages {
        stage('pull image') {  
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh "docker pull gblbjj/${env.APP}:${env.TAG_VERSION}"   
            }
        }
        stage('files') {
            // when { expression { return env.BRANCH == 'develop'} }
            steps {
                git branch: "${env.BRANCH}",
                    url: 'https://github.com/8ball92/deploy_hello_world.git'
            
            }        
                     
        }
        stage('deploy') {
            script {
                def data = readFile(file:  'hello.yml')
                print(data)
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
