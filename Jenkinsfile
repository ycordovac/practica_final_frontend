pipeline{
  agent {
    kubernetes {
        yaml '''

apiVersion: v1
kind: Pod
spec:
  containers:
  - name: shell
    image: yandihlg/jenkins-nodo-nodejs-bootcamp:latest
    volumeMounts:
    - mountPath: /var/run/docker.sock
      name: docker-socket-volume
    securityContext:
      privileged: true
  volumes:
  - name: docker-socket-volume
    hostPath:
      path: /var/run/docker.sock
      type: Socket
    command:
    - sleep
    args:
    - infinity
        '''
        defaultContainer 'shell'
      }
  }

  environment {
    registryCredential='yandihlg'
    registryFrontend = 'yandihlg/angular-14-app'
  }

  stages {
    stage('Build') {
      steps {
        sh 'npm install'
        sh 'npm run build &'
        sleep 20
        sh 'ls -la'
        sh 'cd src'
        sh 'ls -la'
      }
    }

    
  }

  post {
    always {
      sh 'docker logout'
    }
  }
}

