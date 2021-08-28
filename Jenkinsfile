pipeline {
  agent {
    node {
      label 'docker-vm'
    }

  }
  stages {
    stage('CheckOut Code') {
      steps {
        git(url: 'https://github.com/razorbach1/dotnet-core-api.git', branch: 'master', changelog: true, poll: true)
      }
    }

    stage('Build Image Of Docker') {
      steps {
        sh 'docker build -t razotron/todoapi:${BUILD_ID} .'
      }
    }

    stage('Upload Docker Image To Repo') {
      parallel {
        stage('Upload Docker Image To Repo') {
          steps {
            withDockerRegistry(credentialsId: 'docker-hub-creds', url: 'https://index.docker.io/v1/') {
              sh 'docker push razotron/todoapi:${BUILD_ID}'
            }

          }
        }

        stage('Run & Test The Image') {
          steps {
            sh '''docker run -itd -p 80:80 --name todoapi razotron/todoapi:${BUILD_ID}; 
sleep 3s; curl localhost:80; docker stop todoapi; docker rm todoapi'''
          }
        }

      }
    }

  }
}