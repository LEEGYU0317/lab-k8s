pipeline {
    agent {
        kubernetes {
            yaml '''
            apiVersion: v1
            kind: Pod
            spec:
              containers:
              - name: docker
                image: docker:20.10-dind
                securityContext:
                  privileged: true
                command:
                - dockerd-entrypoint.sh
                tty: true
              - name: jnlp
                image: jenkins/inbound-agent:latest
            '''
        }
    }
    
    environment {
        // ★ 아래 주소를 본인의 NCR 엔드포인트로 꼭! 수정해주세요 (따옴표 유지)
        NCR_REGISTRY = 'v5eb64tw.kr.private-ncr.ntruss.com'
        
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
