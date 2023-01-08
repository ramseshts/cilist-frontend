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
                        sh 'docker build -t rafly21/fe-cilistproject:0.0.$BUILD_NUMBER-staging .'
                    }
                }
                else if (env.BRANCH_NAME == 'master') {
                    dir('frontend'){
                         sh 'docker build -t rafly21/fe-cilistproject:0.0.$BUILD_NUMBER-master .' 
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
            sh 'docker push rafly21/fe-cilistproject:0.0.$BUILD_NUMBER-staging'
                }
                else if (env.BRANCH_NAME == 'master') {
            sh 'docker push rafly21/fe-cilistproject:0.0.$BUILD_NUMBER-master' 
                }
                else {
                    sh 'echo Nothing to Push'
                }
        }
      }
    } 
}
     post {
        success {
          if (env.BRANCH_NAME == 'staging' || env.BRANCH_NAME == 'master'){
            slackSend channel: '#devops-channel',
                      color: 'good',
                      message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}"
                }  
            }    
        failure {
          if (env.BRANCH_NAME == 'staging' || env.BRANCH_NAME == 'master'){
            slackSend channel: '#devops-channel',
                      color: 'danger',
                      message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}"
                }
            }
        }   
}


