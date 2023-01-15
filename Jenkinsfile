pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/febfun1/jenkins-k8.git', branch:'main'
      }
    }
    
      stage("Build image") {
            steps {
                    sh 'docker build -t febfun/hellowhale:1.0 .'
                }
            }
        }
    
      stage("Push image") {
            steps {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

    
    stage('Deploy App') {
      steps {
          kubernetesDeploy(configs: "hellowhale.yml", kubeconfigId: "kubernetes")
        }
      }
    }

  }

}
