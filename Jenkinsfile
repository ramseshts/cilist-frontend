pipeline {  
  agent any 
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))   
  }
  stages {
    stage('Build Image Frontend') {
        steps {
            script{
                if (env.BRANCH_NAME == 'staging') {
                    dir('frontend'){
                        sh 'docker build -t ramses01/cilist-frontend:0.0.$BUILD_NUMBER-staging .'
                    }
                }
                else if (env.BRANCH_NAME == 'master') {
                    dir('frontend'){
                         sh 'docker build -t ramses01/cilist-frontend:0.0.$BUILD_NUMBER-master .' 
                    }
                }
                else {
                     sh 'echo Nothing to Build'
                }
            }
        }
    }
    stage('Push to Registry Frontend') {
        steps {
            script {
             if (env.BRANCH_NAME == 'staging') {
            sh 'docker push ramses01/cilist-frontend:0.0.$BUILD_NUMBER-staging'
                }
                else if (env.BRANCH_NAME == 'master') {
            sh 'docker push ramses01/cilist-frontend:0.0.$BUILD_NUMBER-master' 
                }
                else {
                    sh 'echo Nothing to Push'
                }
        }
      }
    } 
  }
}  


