pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/yootaegyun/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t gyun99/cicdtest:green
        sudo docker push gyun99/cicdtest:green
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        sudo kubectl create deploy testpipeline --image=gyun99/cicdtest:green
        sudo kubectl expose deploy testpipeline --type=NodePort --port=80 \
        --target-port=80 --name=testpipeline-svc
        '''
    }
  }
 }
}
