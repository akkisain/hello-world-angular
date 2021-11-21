pipeline {
  agent any
  environment {
  devport = '4200'
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker image build -t akkisain/angularproject:${BUILD_ID} .'
      }
    }

    stage('push image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'mypassword', usernameVariable: 'myusername')]) {
    // some block
          sh '''docker login -u ${myusername} -p ${mypassword}
docker image push akkisain/angularproject:${BUILD_ID}
docker logout
 // docker image rm akkisain/angularproject:${BUILD_ID}'''
        }
        
      }
    }

    stage('deploy on test') {
      steps {
         // sh '''docker context use testserver
  sh 'docker container run -itd -p $devport:8080 akkisain/angularproject:${BUILD_ID}'
 // docker context use default
// '''
      }
    }

    stage('deploy on prod') {
      steps {
    //    sh '''docker context use prodserver
  sh 'docker container run -itd -p  $devport:8080 akkisain/angularproject:${BUILD_ID}'
// docker context use default'''
      }
    }

  }
}
