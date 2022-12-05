pipeline {
    agent {
        node 'k8s-master'
    }
  
    stages {
        stage('Build'){
            steps {
                sh 'echo BUILDING...'
                sh 'echo BUILD ID - ${BUILD_ID}'
                sh 'echo BUILD STAGE OK'
            }
        }
        stage('Test'){
            steps {
                sh 'echo TESTING...'
                sh 'python3 test.py'
            }
        }
        stage('Deploy'){
            steps {
                sh 'echo DEPLOYING...'
                sh 'envsubst < ${WORKSPACE}/wordpress-deployment.yaml'
                sh 'kubectl apply -k ./${WORKSPACE}'
                sh 'watch kubectl get nodes'
                sh 'echo DEPLOY STAGE OK'
            }
        }
    }
}
