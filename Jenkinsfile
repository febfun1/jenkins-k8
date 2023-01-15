pipeline {
    agent any
  
     //create dockerhub credential in github with your dockerhub Username and Password/Token
    environment {
      DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/adeoyedewale/Backend.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                //sh 'npm run build'
            }
        }
	    
        stage('Dockerize') {
            steps {
                sh "docker build -t febfun/nodejs-app:${BUILD_NUMBER} ."
            }
        }
        stage('Publish') {
            steps {
                //sh "docker login -u febfun -p America123"
		sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login --username febfun --password-stdin'
            }
        //stage('Login') {
		
              //steps {
              //   sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login --username febfun --password-stdin'    
             // }
		   // }

        //stage('Push') {

             // steps {
                 //sh 'docker push febfun/nodejs-app:${BUILD_NUMBER}'
             // }
       // }
		}
	}
	
    post {
        always {
	cleanWs()
      	sh 'docker logout'
        }
   }
}
    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "hellowhale.yml", kubeconfigId: "kubernetes")
        }
      }
    }

  }

}
