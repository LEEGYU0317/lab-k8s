pipeline {
  agent {
    kubernetes {
      yaml '''
      apiVersion: v1
      kind: pod
      spec:
        containers:
        - name: docker
          image: docker:20.10-dind
          securityContext:
            privileged: true
          commnad:
          - dockerd-entrypoint.sh
          tty: true
        - name: jnlp
          imageL jenkins/inbound-agent:latest
      '''
    }
  }

  enironment {
    NCR_REGISTRY = 'my-repo.kr.ncr.ntruss.com'
    NCR_CREDENTIAL_ID = 'ncr-credentials'
    IMAGE_NAME = 'my-web-app'
  }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Docker Build') {
            steps {
                container('docker') {
    
    stages {
        stage('Checkout') {
            steps {
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Docker Build') {
            steps {
                container('docker') {
                    sh "docker build -t $NCR_REGISTRY/$IMAGE_NAME:$BUILD_NUMBER ."
                }
            }
        }
        
        stage('Push to NCR') {
            steps {
                container('docker') {
                    withCredentials([usernamePassword(credentialsId: NCR_CREDENTIAL_ID, usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                        sh "echo $PASS | docker login $NCR_REGISTRY -u $USER --password-stdin"
                        sh "docker push $NCR_REGISTRY/$IMAGE_NAME:$BUILD_NUMBER"
                    }
                }
            }
        }
    }
}
                checkout scm
            }
        }
        
        stage('Docker Build') {
            steps {
                container('docker') {
                    sh "docker build -t $NCR_REGISTRY/$IMAGE_NAME:$BUILD_NUMBER ."
                }
            }
        }
        
        stage('Push to NCR') {
            steps {
                container('docker') {
                    withCredentials([usernamePassword(credentialsId: NCR_CREDENTIAL_ID, usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                        sh "echo $PASS | docker login $NCR_REGISTRY -u $USER --password-stdin"
                        sh "docker push $NCR_REGISTRY/$IMAGE_NAME:$BUILD_NUMBER"
                    }
                }
            }
        }
    }
}
                    sh "docker build -t $NCR_REGISTRY/$IMAGE_NAME:$BUILD_NUMBER ."
                }
            }
        }
        
        stage('Push to NCR') {
            steps {
                container('docker') {
                    withCredentials([usernamePassword(credentialsId: NCR_CREDENTIAL_ID, usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                        sh "echo $PASS | docker login $NCR_REGISTRY -u $USER --password-stdin"
                        sh "docker push $NCR_REGISTRY/$IMAGE_NAME:$BUILD_NUMBER"
                    }
                }
            }
        }
    }
}
