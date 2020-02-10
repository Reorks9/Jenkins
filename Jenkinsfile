node{
    stage('SCM Checkout'){
        git credentialsId: 'git-creds', url: 'https://github.com/Reorks9/Jenkins.git'
    }
    stage('Build Docker Image'){
    	sh 'docker build -t reorks9/jenkins:1.0.0 .'
    }
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'docker-pwd', variable: 'DockerHubPwd')]) {
            sh "docker login -u reorks9 -p ${DockerHubPwd}"
        }
        
    	sh 'docker push reorks9/jenkins:1.0.0'
    }
    stage('Run Container'){
    	sh 'docker run -p 8081:8081 -d -v /home/serg/Documents/Jenkins/volumeForJenkins/:/var/lib/jenkins reorks9/jenkins:1.0.0'
    }
}
